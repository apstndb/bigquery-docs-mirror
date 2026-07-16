---
name: documents/docs.cloud.google.com/bigquery/docs/multimodal-data-sql-tutorial
uri: https://docs.cloud.google.com/bigquery/docs/multimodal-data-sql-tutorial
title: Analyze multimodal data with SQL and BigQuery DataFrames
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

# Analyze multimodal data with SQL and BigQuery DataFrames

This tutorial shows you how to [analyze multimodal data](https://docs.cloud.google.com/bigquery/docs/analyze-multimodal-data) by using SQL queries and [BigQuery DataFrames](https://docs.cloud.google.com/bigquery/docs/bigquery-dataframes-introduction) .

This tutorial uses the product catalog from the public Cymbal pet store dataset.

## Objectives

  - Use [`ObjectRef`](https://docs.cloud.google.com/bigquery/docs/work-with-objectref) values to store image data alongside structured data in a BigQuery [standard table](https://docs.cloud.google.com/bigquery/docs/tables-intro#standard-tables) .
  - Enrich your data with image descriptions, keywords, and animal types, and subcategories by using the [`AI.GENERATE` function](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-generate) .
  - Generate embeddings based on image data by using the [`AI.EMBED` function](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-embed) .
  - Find similar images by using the [`VECTOR_SEARCH`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/search_functions#vector_search) function.
  - Summarize user manuals by processing ordered multimodal data using arrays of `ObjectRef` values.

## Costs

In this document, you use the following billable components of Google Cloud:

  - **BigQuery** : you incur costs for the data that you process in BigQuery.
  - **Cloud Storage** : you incur costs for the objects stored in Cloud Storage.
  - **Gemini Enterprise Agent Platform** : you incur costs for calls to Agent Platform models.

To generate a cost estimate based on your projected usage, use the [pricing calculator](https://docs.cloud.google.com/products/calculator) .

New Google Cloud users might be eligible for a [free trial](https://docs.cloud.google.com/free) .

For more information about, see the following pricing pages:

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

  - Create a connection: [BigQuery Connection Admin](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.connectionAdmin) ( `roles/bigquery.connectionAdmin` )
  - Grant permissions to the connection's service account: [Project IAM Admin](https://docs.cloud.google.com/iam/docs/roles-permissions/resourcemanager#resourcemanager.projectIamAdmin) ( `roles/resourcemanager.projectIamAdmin` )
  - Create a Cloud Storage bucket: [Storage Admin](https://docs.cloud.google.com/iam/docs/roles-permissions/storage#storage.admin) ( `roles/storage.admin` )
  - Create datasets, models, UDFs, and tables, and run BigQuery jobs: [BigQuery Admin](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin) ( `roles/bigquery.admin` )
  - Create URLs that let you read and modify Cloud Storage objects: [BigQuery ObjectRef Admin](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.objectRefAdmin) ( `roles/bigquery.objectRefAdmin` )

For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

You might also be able to get the required permissions through [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

## Set up

In this section, you create the dataset, connection, tables, and models used in this tutorial.

### Create a dataset

Create a BigQuery dataset to contain the objects you create in this tutorial:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the left pane, click explore **Explorer** :
    
    ![Highlighted button for the Explorer pane.](https://docs.cloud.google.com/static/bigquery/images/explorer-tab.png)
    
    If you don't see the left pane, click last\_page **Expand left pane** to open the pane.

3.  In the **Explorer** pane, select your project.

4.  Click more\_vert **View actions** , and then click **Create dataset** . The **Create dataset** pane opens.

5.  For **Dataset ID** , type `cymbal_pets` .

6.  Click **Create dataset** .

### Create a connection

Create a [Cloud resource connection](https://docs.cloud.google.com/bigquery/docs/create-cloud-resource-connection) and get the connection's service account. BigQuery uses the connection to access objects in Cloud Storage:

1.  Go to the **BigQuery** page.

2.  In the left pane, click explore **Explorer** :
    
    ![Highlighted button for the Explorer pane.](https://docs.cloud.google.com/static/bigquery/images/explorer-tab.png)

3.  In the **Explorer** pane, click add **Add data** .
    
    The **Add data** dialog opens.

4.  In the **Filter By** pane, in the **Data Source Type** section, select **Business Applications** .
    
    Alternatively, in the **Search for data sources** field, you can enter `Vertex AI` .

5.  In the **Featured data sources** section, click **Vertex AI** .

6.  Click the **Vertex AI Models: BigQuery Federation** solution card.

7.  In the **Connection type** list, select **Vertex AI remote models, remote functions, BigLake and Spanner (Cloud Resource)** .

8.  In the **Connection ID** field, type `cymbal_conn` .

9.  Click **Create connection** .

10. Click **Go to connection** .

11. In the **Connection info** pane, copy the service account ID for use in a following step.

#### Grant permissions to the connection's service account

Grant the connection's service account the appropriate roles to access other services. You must grant these roles in the same project you created or selected in the [Before you begin](https://docs.cloud.google.com/bigquery/docs/multimodal-data-sql-tutorial#before_you_begin) section. Granting the roles in a different project results in the error `bqcx-1234567890-xxxx@gcp-sa-bigquery-condel.iam.gserviceaccount.com does not have the permission to access resource` .

### Create a bucket

Create a Cloud Storage bucket for storing transformed objects:

1.  Go to the **Buckets** page.

2.  Click add\_box **Create** .

3.  On the **Create a bucket** page, in the **Get started** section, enter a globally unique name that meets the [bucket name requirements](https://docs.cloud.google.com/storage/docs/buckets#naming) .

4.  Click **Create** .

#### Grant permissions on the Cloud Storage bucket

Give the service account access to use objects in the bucket you created:

1.  Go to the **Buckets** page.

2.  Click the name of the bucket you created.

3.  Click **Permissions** .

4.  Click person\_add **Grant access** . The **Grant access** dialog opens.

5.  In the **New principals** field, enter the service account ID that you copied earlier.

6.  In the **Select a role** field, choose **Cloud Storage** , and then select **Storage Object User** .

7.  Click **Save** .

#### Grant permissions on to use Agent Platform models

Give the service account access to use Agent Platform models:

1.  Go to the **IAM & Admin** page.

2.  Click person\_add **Grant access** . The **Grant access** dialog opens.

3.  In the **New principals** field, enter the service account ID that you copied earlier.

4.  In the **Select a role** field, enter **Agent Platform User** .

5.  Click **Save** .

### Create the tables of example data

Create tables to store the Cymbal pets product information.

#### Create the `products` table

Create a standard table that contains the Cymbal pets product information:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  Run the following to create the `products` table:
    
    ### SQL
    
        LOAD DATA OVERWRITE cymbal_pets.products
        FROM
          FILES(
            format = 'avro',
            uris = [
              'gs://cloud-samples-data/bigquery/tutorials/cymbal-pets/tables/products/products_*.avro']);
    
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

#### Create the `product_images` table

Create an object table that contains the Cymbal pets product images:

  - Run the following to create the `product_images` table:
    
    ### SQL
    
        CREATE OR REPLACE EXTERNAL TABLE cymbal_pets.product_images
          WITH CONNECTION `us.cymbal_conn`
          OPTIONS (
            object_metadata = 'SIMPLE',
            uris = ['gs://cloud-samples-data/bigquery/tutorials/cymbal-pets/images/*.png'],
            max_staleness = INTERVAL 30 MINUTE,
            metadata_cache_mode = AUTOMATIC);
    
    ### BigQuery DataFrames
    
    Before trying this sample, follow the BigQuery DataFrames setup instructions in the [BigQuery quickstart using BigQuery DataFrames](https://docs.cloud.google.com/bigquery/docs/dataframes-quickstart) . For more information, see the [BigQuery DataFrames reference documentation](https://docs.cloud.google.com/python/docs/reference/bigframes/latest) .
    
    To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up ADC for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .
    
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
        options={"endpoint": "gemini-2.5-flash"},
    )

    embedding_model = bbq.ml.create_model(
        "cymbal_pets.embedding_model",
        replace=True,
        connection_name="us.cymbal_conn",
        options={"endpoint": "multimodalembedding@001"},
    )

## Create a `products_mm` table with multimodal data

Create a `products_mm` table that contains an `image` column populated with product images from the `product_images` object table. The `image` column that is created is a `STRUCT` column that uses the `ObjectRef` format.

1.  Run the following to create the `products_mm` table and populate the `image` column:
    
    ### SQL
    
        CREATE OR REPLACE TABLE cymbal_pets.products_mm
        AS
        SELECT products.* EXCEPT (uri), ot.ref AS image FROM cymbal_pets.products
        INNER JOIN cymbal_pets.product_images ot
        ON ot.uri = products.uri;
    
    ### BigQuery DataFrames
    
    Before trying this sample, follow the BigQuery DataFrames setup instructions in the [BigQuery quickstart using BigQuery DataFrames](https://docs.cloud.google.com/bigquery/docs/dataframes-quickstart) . For more information, see the [BigQuery DataFrames reference documentation](https://docs.cloud.google.com/python/docs/reference/bigframes/latest) .
    
    To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up ADC for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .
    
        df_images = bpd.read_gbq("SELECT * FROM cymbal_pets.product_images")
        df_products = bpd.read_gbq("cymbal_pets.products")
        
        df_products_mm = df_images.merge(df_products, on="uri").drop(columns="uri")
        df_products_mm = df_products_mm.rename(columns={"ref": "image"})

2.  Run the following to view the `image` column data:
    
    ### SQL
    
        SELECT product_name, image
        FROM cymbal_pets.products_mm
    
    ### BigQuery DataFrames
    
    Before trying this sample, follow the BigQuery DataFrames setup instructions in the [BigQuery quickstart using BigQuery DataFrames](https://docs.cloud.google.com/bigquery/docs/dataframes-quickstart) . For more information, see the [BigQuery DataFrames reference documentation](https://docs.cloud.google.com/python/docs/reference/bigframes/latest) .
    
    To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up ADC for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .
    
        df_products_mm[["product_name", "image"]]
    
    The results look similar to the following:
    
    ```console
    +--------------------------------+--------------------------------------+-----------------------------------------------+------------------------------------------------+
    | product_name                   | image.uri                            | image.version | image.authorizer              | image.details                                  |
    +--------------------------------+--------------------------------------+-----------------------------------------------+------------------------------------------------+
    |  AquaClear Aquarium Background | gs://cloud-samples-data/bigquery/    | 1234567891011 | myproject.region.myconnection | {"gcs_metadata":{"content_type":"image/png",   |
    |                                | tutorials/cymbal-pets/images/        |               |                               | "md5_hash":"494f63b9b137975ff3e7a11b060edb1d", |
    |                                | aquaclear-aquarium-background.png    |               |                               | "size":1282805,"updated":1742492680017000}}    |
    +--------------------------------+--------------------------------------+-----------------------------------------------+------------------------------------------------+
    |  AquaClear Aquarium            | gs://cloud-samples-data/bigquery/    | 2345678910112 | myproject.region.myconnection | {"gcs_metadata":{"content_type":"image/png",   |
    |  Gravel Vacuum                 | tutorials/cymbal-pets/images/        |               |                               | "md5_hash":"b7bfc2e2641a77a402a1937bcf0003fd", |
    |                                | aquaclear-aquarium-gravel-vacuum.png |               |                               | "size":820254,"updated":1742492682411000}}     |
    +--------------------------------+--------------------------------------+-----------------------------------------------+------------------------------------------------+
    | ...                            | ...                                  | ...           |                               | ...                                            |
    +--------------------------------+--------------------------------------+-----------------------------------------------+------------------------------------------------+
    ```

## Generate product information

Use the `AI.GENERATE` function to generate the following data for the pet store products:

  - Add an `image_description` column to the `products_mm` table.
  - Populate the `animal_type` , `search_keywords` , and `subcategory` columns of the `products_mm` table.
  - Run a query that returns a description of each product brand and also a count of the number of products from that brand. The brand description is generated by analyzing product information for all of the products from that brand, including product images.

<!-- end list -->

1.  Run the following to create and populate the `image_description` column:
    
    ### SQL
    
        CREATE OR REPLACE TABLE cymbal_pets.products_mm AS (
          SELECT
            *, AI.GENERATE(('Describe the following image: ', image), endpoint => 'gemini-2.5-pro').result AS image_description
          FROM
            cymbal_pets.products_mm
        );
    
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

2.  Run the following to update the `animal_type` , `search_keywords` , and `subcategory` columns with generated data:
    
    ### SQL
    
        CREATE OR REPLACE TABLE cymbal_pets.products_mm AS (
        SELECT * EXCEPT(animal_type, search_keywords, subcategory),
          AI.GENERATE(
            ('For the image and description of a pet product, concisely generate the following metadata: '
            '1) animal_type and 2) 5 SEO search keywords, and 3) product subcategory. ',
            image,
            description),
            endpoint => 'gemini-2.5-pro',
            output_schema => 'animal_type STRING, search_keywords ARRAY, subcategory STRING').*
        FROM cymbal_pets.products_mm);
    
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

3.  Run the following to view the generated data:
    
    ### SQL
    
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
    
    The results look similar to the following:
    
    ```console
    +--------------------------------+-------------------------------------+-------------+------------------------+------------------+
    | product_name                   | image.description                   | animal_type | search_keywords        | subcategory      |
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

4.  Run the following to generate a description of each product brand and also a count of the number of products from that brand:
    
    ### SQL
    
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
    
    The results look similar to the following:
    
    ```console
    +--------------+-------------------------------------+-----+
    | brand        | brand.description                   | cnt |
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

In a production scenario, we recommend creating a [vector index](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_vector_index_statement) before running a vector search. A vector index lets you perform the vector search more quickly, with the trade-off of reducing recall and so returning more approximate results.

1.  Run the following to create the `products_embeddings` table:
    
    ### SQL
    
        CREATE OR REPLACE TABLE cymbal_pets.products_embedding
        AS (
          SELECT
            product_id,
            AI.EMBED(image, endpoint => 'multimodalembedding@001').result AS embedding,
            image
          FROM cymbal_pets.products_mm
        );
    
    ### BigQuery DataFrames
    
    Before trying this sample, follow the BigQuery DataFrames setup instructions in the [BigQuery quickstart using BigQuery DataFrames](https://docs.cloud.google.com/bigquery/docs/dataframes-quickstart) . For more information, see the [BigQuery DataFrames reference documentation](https://docs.cloud.google.com/python/docs/reference/bigframes/latest) .
    
    To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up ADC for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .
    
        df_products_mm["content"] = bbq.obj.get_access_url(df_products_mm["image"], "R")
        df_embed = bbq.ai.generate_embedding(
            embedding_model, df_products_mm[["content", "product_id"]]
        )
        
        df_embed.to_gbq("cymbal_pets.products_embedding", if_exists="replace")

2.  Run the following to run a vector search to return product images that are similar to the given input image:
    
    ### SQL
    
        SELECT *
        FROM
          VECTOR_SEARCH(
            TABLE cymbal_pets.products_embedding,
            'embedding',
            query_value => AI.EMBED(
                            OBJ.MAKE_REF('gs://cloud-samples-data/bigquery/tutorials/cymbal-pets/images/cozy-naps-cat-scratching-post-with-condo.png'),
                            endpoint => 'multimodalembedding@001').result);
    
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

This section shows you how to complete the following tasks:

1.  Create the `product_manuals` table so that it contains both a PDF file for the `Crittercuisine Pro 5000` product manual, and PDF files for each page of that manual.
2.  Create a table that maps the manual to its chunks. The complete manual and the manual pages are each stored in an `ObjectRef` column.
3.  Analyze an array of `ObjectRef` values together to return a single generated value.
4.  Analyze an array of `ObjectRef` values separately and returning a generated value for each array value.

Follow these steps to process ordered multimodal data using `ObjectRef` values:

1.  Go to the **BigQuery** page.

2.  Run the following to create the `product_manuals` table:
    
    ### SQL
    
        CREATE OR REPLACE EXTERNAL TABLE `cymbal_pets.product_manuals`
          WITH CONNECTION `us.cymbal_conn`
          OPTIONS (
            object_metadata = 'SIMPLE',
            uris = [
                'gs://cloud-samples-data/bigquery/tutorials/cymbal-pets/documents/*.pdf',
                'gs://cloud-samples-data/bigquery/tutorials/cymbal-pets/document_chunks/*.pdf']);
    
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

3.  Run the following to write PDF data to the `map_manual_to_chunks` table:
    
    ### SQL
    
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

4.  Run the following to view the PDF data in the `map_manual_to_chunks` table:
    
    ### SQL
    
        SELECT *
        FROM cymbal_pets.map_manual_to_chunks;
    
    ### BigQuery DataFrames
    
    Before trying this sample, follow the BigQuery DataFrames setup instructions in the [BigQuery quickstart using BigQuery DataFrames](https://docs.cloud.google.com/bigquery/docs/dataframes-quickstart) . For more information, see the [BigQuery DataFrames reference documentation](https://docs.cloud.google.com/python/docs/reference/bigframes/latest) .
    
    To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up ADC for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .
    
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

5.  Run the following to generate a single response from a Gemini model based on the analysis of an array of `ObjectRef` values:
    
    ### SQL
    
        SELECT
          AI.GENERATE((
            '''Can you provide a page by page summary for the first 3 pages of the attached manual?
            Only write one line for each page. The pages are provided in serial order''',
            chunks),
            endpoint => 'gemini-2.5-pro').result AS Response,
        FROM cymbal_pets.map_manual_to_chunks
    
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

6.  Run the following to generate multiple responses from a Gemini model based on the analysis of an array of `ObjectRef` values:
    
    ### SQL
    
        WITH results AS (
          SELECT
            AI.GENERATE((
              '''Can you provide a page by page summary for the first 3 pages of the attached manual?
              Only write one line for each page. The pages are provided in serial order''',
              chunks),
              endpoint => 'gemini-2.5-pro'
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

> **Caution** : Deleting a project has the following effects:
> 
>   - **Everything in the project is deleted.** If you used an existing project for the tasks in this document, when you delete it, you also delete any other work you've done in the project.
>   - **Custom project IDs are lost.** When you created this project, you might have created a custom project ID that you want to use in the future. To preserve the URLs that use the project ID, such as an `appspot.com` URL, delete selected resources inside the project instead of deleting the whole project.
> 
> If you plan to explore multiple architectures, tutorials, or quickstarts, reusing projects can help you avoid exceeding project quota limits.

In the Google Cloud console, go to the **Manage resources** page.

In the project list, select the project that you want to delete, and then click **Delete** .

In the dialog, type the project ID, and then click **Shut down** to delete the project.
