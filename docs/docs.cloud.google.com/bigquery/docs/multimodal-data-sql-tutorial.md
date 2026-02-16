# Analyze multimodal data with SQL and Python UDFs

**Preview**

This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

**Note:** To provide feedback or request support for this feature, send an email to <bq-objectref-feedback@google.com> .

This tutorial shows you how to [analyze multimodal data](/bigquery/docs/analyze-multimodal-data) by using SQL queries and [Python user-defined functions (UDFs)](/bigquery/docs/user-defined-functions-python) .

This tutorial uses the product catalog from the public Cymbal pet store dataset.

## Objectives

  - Use [`  ObjectRef  `](/bigquery/docs/reference/standard-sql/objectref_functions#objectref) values to store image data alongside structured data in a BigQuery [standard table](/bigquery/docs/tables-intro#standard-tables) .
  - Generate text based on image data from a standard table by using the [`  AI.GENERATE_TABLE  ` function](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-generate-table) .
  - Transform existing images to create new images by using a Python UDF.
  - Chunk PDFs for further analysis by using a Python UDF.
  - Use a Gemini model and the `  AI.GENERATE_TEXT  ` function to analyze the chunked PDF data.
  - Generate embeddings based on image data from a standard table by using the [`  AI.GENERATE_EMBEDDING  ` function](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-generate-embedding) .
  - Process ordered multimodal data using arrays of `  ObjectRef  ` values.

## Costs

In this document, you use the following billable components of Google Cloud:

  - **BigQuery** : you incur costs for the data that you process in BigQuery.
  - **BigQuery Python UDFs** : you incur costs for using Python UDFs.
  - **Cloud Storage** : you incur costs for the objects stored in Cloud Storage.
  - **Vertex AI** : you incur costs for calls to Vertex AI models.

To generate a cost estimate based on your projected usage, use the [pricing calculator](/products/calculator) .

New Google Cloud users might be eligible for a [free trial](/free) .

For more information about, see the following pricing pages:

  - [BigQuery pricing](https://cloud.google.com/bigquery/pricing)
  - [BigQuery Python UDFs pricing](/bigquery/docs/user-defined-functions-python#pricing)
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
  - Create datasets, models, UDFs, and tables, and run BigQuery jobs: [BigQuery Admin](/iam/docs/roles-permissions/bigquery#bigquery.admin) ( `  roles/bigquery.admin  ` )
  - Create URLs that let you read and modify Cloud Storage objects: [BigQuery ObjectRef Admin](/iam/docs/roles-permissions/bigquery#bigquery.objectRefAdmin) ( `  roles/bigquery.objectRefAdmin  ` )

For more information about granting roles, see [Manage access to projects, folders, and organizations](/iam/docs/granting-changing-revoking-access) .

You might also be able to get the required permissions through [custom roles](/iam/docs/creating-custom-roles) or other [predefined roles](/iam/docs/roles-overview#predefined) .

## Set up

In this section, you create the dataset, connection, tables, and models used in this tutorial.

### Create a dataset

Create a BigQuery dataset to contain the objects you create in this tutorial:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the left pane, click explore **Explorer** :
    
    If you don't see the left pane, click last\_page **Expand left pane** to open the pane.

3.  In the **Explorer** pane, select your project.

4.  Click more\_vert **View actions** , and then click **Create dataset** . The **Create dataset** pane opens.

5.  For **Dataset ID** , type `  cymbal_pets  ` .

6.  Click **Create dataset** .

### Create a bucket

Create a Cloud Storage bucket for storing transformed objects:

1.  Go to the **Buckets** page.

2.  Click add\_box **Create** .

3.  On the **Create a bucket** page, in the **Get started** section, enter a globally unique name that meets the [bucket name requirements](/storage/docs/buckets#naming) .

4.  Click **Create** .

### Create a connection

Create a [Cloud resource connection](/bigquery/docs/create-cloud-resource-connection) and get the connection's service account. BigQuery uses the connection to access objects in Cloud Storage:

1.  Go to the **BigQuery** page.

2.  In the left pane, click explore **Explorer** :

3.  In the **Explorer** pane, click add **Add data** .
    
    The **Add data** dialog opens.

4.  In the **Filter By** pane, in the **Data Source Type** section, select **Business Applications** .
    
    Alternatively, in the **Search for data sources** field, you can enter `  Vertex AI  ` .

5.  In the **Featured data sources** section, click **Vertex AI** .

6.  Click the **Vertex AI Models: BigQuery Federation** solution card.

7.  In the **Connection type** list, select **Vertex AI remote models, remote functions, BigLake and Spanner (Cloud Resource)** .

8.  In the **Connection ID** field, type `  cymbal_conn  ` .

9.  Click **Create connection** .

10. Click **Go to connection** .

11. In the **Connection info** pane, copy the service account ID for use in a following step.

### Grant permissions to the connection's service account

Grant the connection's service account the appropriate roles to access other services. You must grant these roles in the same project you created or selected in the [Before you begin](#before_you_begin) section. Granting the roles in a different project results in the error `  bqcx-1234567890-xxxx@gcp-sa-bigquery-condel.iam.gserviceaccount.com does not have the permission to access resource  ` .

#### Grant permissions on the Cloud Storage bucket

Give the service account access to use objects in the bucket you created:

1.  Go to the **Buckets** page.

2.  Click the name of the bucket you created.

3.  Click **Permissions** .

4.  Click person\_add **Grant access** . The **Grant access** dialog opens.

5.  In the **New principals** field, enter the service account ID that you copied earlier.

6.  In the **Select a role** field, choose **Cloud Storage** , and then select **Storage Object User** .

7.  Click **Save** .

#### Grant permissions on to use Vertex AI models

Give the service account access to use Vertex AI models:

1.  Go to the **IAM & Admin** page.

2.  Click person\_add **Grant access** . The **Grant access** dialog opens.

3.  In the **New principals** field, enter the service account ID that you copied earlier.

4.  In the **Select a role** field, select **Vertex AI** , and then select **Vertex AI User** .

5.  Click **Save** .

### Create the tables of example data

Create tables to store the Cymbal pets product information.

#### Create the `     products    ` table

Create a standard table that contains the Cymbal pets product information:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, run the following query to create the `  products  ` table:
    
    ``` text
    LOAD DATA OVERWRITE cymbal_pets.products
    FROM
      FILES(
        format = 'avro',
        uris = [
          'gs://cloud-samples-data/bigquery/tutorials/cymbal-pets/tables/products/products_*.avro']);
    ```

#### Create the `     product_images    ` table

Create an object table that contains the Cymbal pets product images:

  - In the query editor of the **BigQuery** page, run the following query to create the `  product_images  ` table:
    
    ``` text
    CREATE OR REPLACE EXTERNAL TABLE cymbal_pets.product_images
      WITH CONNECTION `us.cymbal_conn`
      OPTIONS (
        object_metadata = 'SIMPLE',
        uris = ['gs://cloud-samples-data/bigquery/tutorials/cymbal-pets/images/*.png'],
        max_staleness = INTERVAL 30 MINUTE,
        metadata_cache_mode = AUTOMATIC);
    ```

#### Create the `     product_manuals    ` table

Create an object table that contains the Cymbal pets product manuals:

  - In the query editor of the **BigQuery** page, run the following query to create the `  product_manuals  ` table:
    
    ``` text
    CREATE OR REPLACE EXTERNAL TABLE cymbal_pets.product_manuals
      WITH CONNECTION `us.cymbal_conn`
      OPTIONS (
        object_metadata = 'SIMPLE',
        uris = ['gs://cloud-samples-data/bigquery/tutorials/cymbal-pets/documents/*.pdf']);
    ```

### Create a text generation model

Create a BigQuery ML [remote model](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model) that represents a Vertex AI Gemini model:

  - In the query editor of the **BigQuery** page, run the following query to create the remote model:
    
    ``` text
    CREATE OR REPLACE MODEL `cymbal_pets.gemini`
      REMOTE WITH CONNECTION `us.cymbal_conn`
      OPTIONS (ENDPOINT = 'gemini-2.0-flash');
    ```

### Create an embedding generation model

Create a BigQuery ML remote model that represents a Vertex AI multimodal embedding model:

  - In the query editor of the **BigQuery** page, run the following query to create the remote model:
    
    ``` text
    CREATE OR REPLACE MODEL `cymbal_pets.embedding_model`
      REMOTE WITH CONNECTION `us.cymbal_conn`
      OPTIONS (ENDPOINT = 'multimodalembedding@001');
    ```

## Create a `     products_mm    ` table with multimodal data

Create a `  products_mm  ` table that contains an `  image  ` column populated with product images from the `  product_images  ` object table. The `  image  ` column that is created is a `  STRUCT  ` column that uses the `  ObjectRef  ` format.

1.  In the query editor of the **BigQuery** page, run the following query to create the `  products_mm  ` table and populate the `  image  ` column:
    
    ``` text
    CREATE OR REPLACE TABLE cymbal_pets.products_mm
    AS
    SELECT products.* EXCEPT (uri), ot.ref AS image FROM cymbal_pets.products
    INNER JOIN cymbal_pets.product_images ot
    ON ot.uri = products.uri;
    ```

2.  In the query editor of the **BigQuery** page, run the following query to view the `  image  ` column data:
    
    ``` text
    SELECT product_name, image
    FROM cymbal_pets.products_mm
    ```
    
    The results look similar to the following:
    
    ``` console
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

## Generate product information by using a Gemini model

Use a Gemini model to generate the following data for the pet store products:

  - Add an `  image_description  ` column to the `  products_mm  ` table.
  - Populate the `  animal_type  ` , `  search_keywords  ` , and `  subcategory  ` columns of the `  products_mm  ` table.
  - Run a query that returns a description of each product brand and also a count of the number of products from that brand. The brand description is generated by analyzing product information for all of the products from that brand, including product images.

<!-- end list -->

1.  In the query editor of the **BigQuery** page, run the following query to create and populate the `  image_description  ` column:
    
    ``` text
    CREATE OR REPLACE TABLE cymbal_pets.products_mm
    AS
    SELECT
      product_id,
      product_name,
      brand,
      category,
      subcategory,
      animal_type,
      search_keywords,
      price,
      description,
      inventory_level,
      supplier_id,
      average_rating,
      image,
      image_description
    FROM
      AI.GENERATE_TABLE(
        MODEL `cymbal_pets.gemini`,
        (
          SELECT
            ('Can you describe the following image? ', OBJ.GET_ACCESS_URL(image, 'r')) AS prompt,
            *
          FROM
            cymbal_pets.products_mm
        ),
        STRUCT('image_description STRING' AS output_schema));
    ```

2.  In the query editor of the **BigQuery** page, run the following query to update the `  animal_type  ` , `  search_keywords  ` , and `  subcategory  ` columns with generated data:
    
    ``` text
    UPDATE cymbal_pets.products_mm p
    SET
      p.animal_type = s.animal_type,
      p.search_keywords = s.search_keywords,
      p.subcategory = s.subcategory
    FROM
      (
        SELECT
          animal_type,
          search_keywords,
          subcategory,
          uri
        FROM
          AI.GENERATE_TABLE(
            MODEL `cymbal_pets.gemini`,
            (
              SELECT
                (
                  'For the image of a pet product, concisely generate the following metadata: '
                  '1) animal_type and 2) 5 SEO search keywords, and 3) product subcategory. ',
                  OBJ.GET_ACCESS_URL(image, 'r'),
                  description) AS prompt,
                image.uri AS uri,
              FROM cymbal_pets.products_mm
            ),
            STRUCT(
              'animal_type STRING, search_keywords ARRAY<STRING>, subcategory STRING' AS output_schema,
              100 AS max_output_tokens))
      ) s
    WHERE p.image.uri = s.uri;
    ```

3.  In the query editor of the **BigQuery** page, run the following query to view the generated data:
    
    ``` text
    SELECT
      product_name,
      image_description,
      animal_type,
      search_keywords,
      subcategory,
    FROM cymbal_pets.products_mm;
    ```
    
    The results look similar to the following:
    
    ``` console
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

4.  In the query editor of the **BigQuery** page, run the following query to generate a description of each product brand and also a count of the number of products from that brand:
    
    ``` text
    SELECT
      brand,
      brand_description,
      cnt
    FROM
      AI.GENERATE_TABLE(
        MODEL `cymbal_pets.gemini`,
        (
          SELECT
            brand,
            COUNT(*) AS cnt,
            (
              'Use the images and text to give one concise brand description for a website brand page.'
                'Return the description only. ',
              ARRAY_AGG(OBJ.GET_ACCESS_URL(image, 'r')), ' ',
              ARRAY_AGG(description), ' ',
              ARRAY_AGG(category), ' ',
              ARRAY_AGG(subcategory)) AS prompt
          FROM cymbal_pets.products_mm
          GROUP BY brand
        ),
        STRUCT('brand_description STRING' AS output_schema))
    ORDER BY cnt DESC;
    ```
    
    The results look similar to the following:
    
    ``` console
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

## Create a Python UDF to transform product images

Create a Python UDF to convert product images to grayscale.

The Python UDF uses open source libraries , and also uses parallel execution to transform multiple images simultaneously.

1.  In the query editor of the **BigQuery** page, run the following query to create the `  to_grayscale  ` UDF:
    
    ``` text
    CREATE OR REPLACE FUNCTION cymbal_pets.to_grayscale(src_json STRING, dst_json STRING)
    RETURNS STRING
    LANGUAGE python
    WITH CONNECTION `us.cymbal_conn`
    OPTIONS (entry_point='to_grayscale', runtime_version='python-3.11', packages=['numpy', 'opencv-python'])
    AS """
    
    import cv2 as cv
    import numpy as np
    from urllib.request import urlopen, Request
    import json
    
    # Transform the image to grayscale.
    def to_grayscale(src_ref, dst_ref):
      src_json = json.loads(src_ref)
      srcUrl = src_json["access_urls"]["read_url"]
    
      dst_json = json.loads(dst_ref)
      dstUrl = dst_json["access_urls"]["write_url"]
    
      req = urlopen(srcUrl)
      arr = np.asarray(bytearray(req.read()), dtype=np.uint8)
      img = cv.imdecode(arr, -1) # 'Load it as it is'
    
      # Convert the image to grayscale
      gray_image = cv.cvtColor(img, cv.COLOR_BGR2GRAY)
    
      # Send POST request to the URL
      _, img_encoded = cv.imencode('.png', gray_image)
    
      req = Request(url=dstUrl, data=img_encoded.tobytes(), method='PUT', headers = {
          "Content-Type": "image/png",
      })
      with urlopen(req) as f:
          pass
      return dst_ref
    """;
    ```

## Transform product images

Create the `  products_grayscale  ` table with an `  ObjectRef  ` column that contains the destination paths and authorizers for grayscale images. The destination path is derived from the original image path.

After you create the table, run the `  to_grayscale  ` function to create the grayscale images, write them to a Cloud Storage bucket, and then return [`  ObjectRefRuntime  `](/bigquery/docs/reference/standard-sql/objectref_functions#objectrefruntime) values containing access URLs and metadata for the grayscale images.

1.  In the query editor of the **BigQuery** page, run the following query to create the `  products_grayscale  ` table:
    
    ``` text
    CREATE OR REPLACE TABLE cymbal_pets.products_grayscale
    AS
    SELECT
      product_id,
      product_name,
      image,
      OBJ.MAKE_REF(
        CONCAT('gs://BUCKET/cymbal-pets-images/grayscale/', REGEXP_EXTRACT(image.uri, r'([^/]+)$')),
        'us.cymbal_conn') AS gray_image
    FROM cymbal_pets.products_mm;
    ```
    
    Replace `  BUCKET  ` with the name of the [bucket that you created](#create_a_bucket) .

2.  In the query editor of the **BigQuery** page, run the following query to create the grayscale images, write them to a Cloud Storage bucket, and then return `  ObjectRefRuntime  ` values containing access URLs and metadata for the grayscale images:
    
    ``` text
    SELECT cymbal_pets.to_grayscale(
      TO_JSON_STRING(OBJ.GET_ACCESS_URL(image, 'r')),
      TO_JSON_STRING(OBJ.GET_ACCESS_URL(gray_image, 'rw')))
    FROM cymbal_pets.products_grayscale;
    ```
    
    The results look similar to the following:
    
    ``` console
    +-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
    | f0                                                                                                                                                                    |
    +-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
    | {"access_urls":{"expiry_time":"2025-04-26T03:00:48Z",                                                                                                                 |
    | "read_url":"https://storage.googleapis.com/mybucket/cymbal-pets-images%2Fgrayscale%2Focean-bites-salmon-%26-tuna-cat-food.png?additional_read URL_information",       |
    | "write_url":"https://storage.googleapis.com/myproject/cymbal-pets-images%2Fgrayscale%2Focean-bites-salmon-%26-tuna-cat-food.png?additional_write URL_information"},   |
    | "objectref":{"authorizer":"myproject.region.myconnection","uri":"gs://myproject/cymbal-pets-images/grayscale/ocean-bites-salmon-&-tuna-cat-food.png"}}                |
    +-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
    | {"access_urls":{"expiry_time":"2025-04-26T03:00:48Z",                                                                                                                 |
    | "read_url":"https://storage.googleapis.com/mybucket/cymbal-pets-images%2Fgrayscale%2Ffluffy-buns-guinea-pig-tunnel.png?additional _read URL_information",             |
    | "write_url":"https://storage.googleapis.com/myproject/cymbal-pets-images%2Fgrayscale%2Focean-bites-salmon-%26-tuna-cat-food.png?additional_write_URL_information"},   |
    | "objectref":{"authorizer":"myproject.region.myconnection","uri":"gs://myproject/cymbal-pets-images%2Fgrayscale%2Ffluffy-buns-guinea-pig-tunnel.png"}}                 |
    +-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
    |  ...                                                                                                                                                                  |
    +-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
    ```

## Create a Python UDF to chunk PDF data

Create a Python UDF to chunk the PDF objects that contain the Cymbal pets product manuals into multiple parts.

PDFs are often very large and might not fit into a single call to a generative AI model. By chunking the PDFs, you can store the PDF data in a model-ready format for easier analysis.

1.  In the query editor of the **BigQuery** page, run the following query to create the `  chunk_pdf  ` UDF:
    
    ``` text
    -- This function chunks the product manual PDF into multiple parts.
    -- The function accepts an ObjectRefRuntime value for the PDF file and the chunk size.
    -- It then parses the PDF, chunks the contents, and returns an array of chunked text.
    CREATE OR REPLACE FUNCTION cymbal_pets.chunk_pdf(src_json STRING, chunk_size INT64, overlap_size INT64)
    RETURNS ARRAY<STRING>
    LANGUAGE python
    WITH CONNECTION `us.cymbal_conn`
    OPTIONS (entry_point='chunk_pdf', runtime_version='python-3.11', packages=['pypdf'])
    AS """
    import io
    import json
    
    from pypdf import PdfReader  # type: ignore
    from urllib.request import urlopen, Request
    
    def chunk_pdf(src_ref: str, chunk_size: int, overlap_size: int) -> str:
      src_json = json.loads(src_ref)
      srcUrl = src_json["access_urls"]["read_url"]
    
      req = urlopen(srcUrl)
      pdf_file = io.BytesIO(bytearray(req.read()))
      reader = PdfReader(pdf_file, strict=False)
    
      # extract and chunk text simultaneously
      all_text_chunks = []
      curr_chunk = ""
      for page in reader.pages:
          page_text = page.extract_text()
          if page_text:
              curr_chunk += page_text
              # split the accumulated text into chunks of a specific size with overlaop
              # this loop implements a sliding window approach to create chunks
              while len(curr_chunk) >= chunk_size:
                  split_idx = curr_chunk.rfind(" ", 0, chunk_size)
                  if split_idx == -1:
                      split_idx = chunk_size
                  actual_chunk = curr_chunk[:split_idx]
                  all_text_chunks.append(actual_chunk)
                  overlap = curr_chunk[split_idx + 1 : split_idx + 1 + overlap_size]
                  curr_chunk = overlap + curr_chunk[split_idx + 1 + overlap_size :]
      if curr_chunk:
          all_text_chunks.append(curr_chunk)
    
      return all_text_chunks
    """;
    ```

## Analyze PDF data

Run the `  chunk_pdf  ` function to chunk the PDF data in the `  product_manuals  ` table, and then create a `  product_manual_chunk_strings  ` table that contains one PDF chunk per row. Use a Gemini model on the `  product_manual_chunk_strings  ` data to summarize the legal information found in the product manuals.

1.  In the query editor of the **BigQuery** page, run the following query to create the `  product_manual_chunk_strings  ` table:
    
    ``` text
    CREATE OR REPLACE TABLE cymbal_pets.product_manual_chunk_strings
    AS
    SELECT chunked
    FROM cymbal_pets.product_manuals,
    UNNEST (cymbal_pets.chunk_pdf(
      TO_JSON_STRING(
        OBJ.GET_ACCESS_URL(OBJ.MAKE_REF(uri, 'us.cymbal_conn'), 'r')),
        1000,
        100
    )) as chunked;
    ```

2.  In the query editor of the **BigQuery** page, run the following query to analyze the PDF data by using a Gemini model:
    
    ``` text
    SELECT
      result
    FROM
      AI.GENERATE_TEXT(
        MODEL `cymbal_pets.gemini`,
        (
          SELECT
            (
              'Can you summarize the product manual as bullet points? Highlight the legal clauses',
              chunked) AS prompt,
          FROM cymbal_pets.product_manual_chunk_strings
        ));
    ```
    
    The results look similar to the following:
    
    ``` console
    +-------------------------------------------------------------------------------------------------------------------------------------------+
    | result                                                                                                                                    |
    +-------------------------------------------------------------------------------------------------------------------------------------------+
    | ## CritterCuisine Pro 5000 Automatic Pet Feeder Manual Summary:                                                                           |
    |                                                                                                                                           |
    | **Safety:**                                                                                                                               |
    |                                                                                                                                           |
    | * **Stability:** Place feeder on a level, stable surface to prevent tipping.                                                              |
    | * **Power Supply:** Only use the included AC adapter. Using an incompatible adapter can damage the unit and void the warranty.            |
    | * **Cord Safety:** Keep the power cord out of reach of pets to prevent chewing or entanglement.                                           |
    | * **Children:** Supervise children around the feeder. This is not a toy.                                                                  |
    | * **Pet Health:** Consult your veterinarian before using an automatic feeder if your pet has special dietary needs, health conditions, or |
    +-------------------------------------------------------------------------------------------------------------------------------------------+
    | ## Product Manual Summary:                                                                                                                |
    |                                                                                                                                           |
    | **6.3 Manual Feeding:**                                                                                                                   |
    |                                                                                                                                           |
    | * Press MANUAL button to dispense a single portion (Meal 1 size). **(Meal Enabled)**                                                      |
    |                                                                                                                                           |
    | **6.4 Recording a Voice Message:**                                                                                                        |
    |                                                                                                                                           |
    | * Press and hold VOICE button.                                                                                                            |
    | * Speak clearly into the microphone (up to 10 seconds).                                                                                   |
    | * Release VOICE button to finish recording.                                                                                               |
    | * Briefly press VOICE button to play back the recording.                                                                                  |
    | * To disable the voice message, record a blank message (hold VOICE button for 10 seconds without speaking). **(Meal Enabled)**            |
    |                                                                                                                                           |
    | **6.5 Low Food Level Indicator:**                                                                                                         |
    +-------------------------------------------------------------------------------------------------------------------------------------------+
    | ...                                                                                                                                       |
    +-------------------------------------------------------------------------------------------------------------------------------------------+
    ```

## Generate embeddings and perform a vector search

Generate embeddings from image data, and then use the embeddings to return similar images by using [vector search](/bigquery/docs/vector-search-intro) .

In a production scenario, we recommend creating a [vector index](/bigquery/docs/reference/standard-sql/data-definition-language#create_vector_index_statement) before running a vector search. A vector index lets you perform the vector search more quickly, with the trade-off of reducing recall and so returning more approximate results.

1.  In the query editor of the **BigQuery** page, run the following query to create the `  products_embeddings  ` table:
    
    ``` text
    CREATE OR REPLACE TABLE cymbal_pets.products_embedding
    AS
    SELECT product_id, embedding, content as image
    FROM AI.GENERATE_EMBEDDING(
    MODEL `cymbal_pets.embedding_model`,
      (
        SELECT OBJ.GET_ACCESS_URL(image, 'r') as content, image, product_id
        FROM cymbal_pets.products_mm
      )
    );
    ```

2.  In the query editor of the **BigQuery** page, run the following query to run a vector search to return product images that are similar to the given input image:
    
    ``` text
    SELECT *
    FROM
    VECTOR_SEARCH(
      TABLE cymbal_pets.products_embedding,
      'embedding',
      (SELECT embedding FROM AI.GENERATE_EMBEDDING(
        MODEL `cymbal_pets.embedding_model`,
        (SELECT OBJ.FETCH_METADATA(OBJ.MAKE_REF('gs://cloud-samples-data/bigquery/tutorials/cymbal-pets/images/cozy-naps-cat-scratching-post-with-condo.png', 'us.cymbal_conn')) as content)
      ))
    );
    ```
    
    The results look similar to the following:
    
    ``` console
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
    +---------C--------+-----------------+----------------+----------------------------------------------+--------------------+-------------------------------+------------------------------------------------+----------------+
    | ...             | ...             | ...            | ...                                          | ...                | ...                           | ...                                            | ...            |
    +-----------------+-----------------+----------------+----------------------------------------------+--------------------+-------------------------------+------------------------------------------------+----------------+
    ```

## Process ordered multimodal data using arrays of `     ObjectRef    ` values

This section shows you how to complete the following tasks:

1.  Recreate the `  product_manuals  ` table so that it contains both a PDF file for the `  Crittercuisine 5000  ` product manual, and PDF files for each page of that manual.
2.  Create a table that maps the manual to its chunks. The `  ObjectRef  ` value that represents the complete manual is stored in a `  STRUCT<uri STRING, version STRING, authorizer STRING, details JSON>>  ` column. The `  ObjectRef  ` values that represent the manual pages are stored in an `  ARRAY<STRUCT<uri STRING, version STRING, authorizer STRING, details JSON>>  ` column.
3.  Analyze an array of `  ObjectRef  ` values together to return a single generated value.
4.  Analyze an array of `  ObjectRef  ` values separately and returning a generated value for each array value.

As part of the analysis tasks, you convert the array of `  ObjectRef  ` values to an ordered list of [`  ObjectRefRuntime  `](/bigquery/docs/analyze-multimodal-data#objectrefruntime_values) values, and then pass that list to a Gemini model, specifying the `  ObjectRefRuntime  ` values as part of the prompt. The `  ObjectRefRuntime  ` values provide signed URLs that the model uses to access the object information in Cloud Storage.

Follow these steps to process ordered multimodal data using arrays of `  ObjectRef  ` values:

1.  Go to the **BigQuery** page.

2.  In the query editor, run the following query to recreate the `  product_manuals  ` table:
    
    ``` text
    CREATE OR REPLACE EXTERNAL TABLE `cymbal_pets.product_manuals`
      WITH CONNECTION `us.cymbal_conn`
      OPTIONS (
        object_metadata = 'SIMPLE',
        uris = [
            'gs://cloud-samples-data/bigquery/tutorials/cymbal-pets/documents/*.pdf',
            'gs://cloud-samples-data/bigquery/tutorials/cymbal-pets/document_chunks/*.pdf']);
    ```

3.  In the query editor, run the following query to write PDF data to the `  map_manual_to_chunks  ` table:
    
    ``` text
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
    ```

4.  In the query editor, run the following query to view the PDF data in the `  map_manual_to_chunks  ` table:
    
    ``` text
    SELECT *
    FROM cymbal_pets.map_manual_to_chunks;
    ```
    
    The results look similar to the following:
    
    ``` console
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

5.  In the query editor, run the following query to generate a single response from a Gemini model based on the analysis of an array of `  ObjectRef  ` values:
    
    ``` text
    WITH
      manuals AS (
        SELECT
          OBJ.GET_ACCESS_URL(manual, 'r') AS manual,
          ARRAY(
            SELECT OBJ.GET_ACCESS_URL(chunk, 'r') AS chunk
            FROM UNNEST(m1.chunks) AS chunk WITH OFFSET AS idx
            ORDER BY idx
          ) AS chunks
        FROM cymbal_pets.map_manual_to_chunks AS m1
      )
    SELECT result AS Response
    FROM
      AI.GENERATE_TEXT(
        MODEL `cymbal_pets.gemini`,
        (
          SELECT
            (
              'Can you provide a page by page summary for the first 3 pages of the attached manual? Only write one line for each page. The pages are provided in serial order',
              manuals.chunks) AS prompt,
          FROM manuals
        ));
    ```
    
    The results look similar to the following:
    
    ``` console
    +-------------------------------------------+
    | Response                                  |
    +-------------------------------------------+
    | Page 1: This manual is for the            |
    | CritterCuisine Pro 5000 automatic         |
    | pet feeder.                               |
    | Page 2: The manual covers safety          |
    | precautions, what's included,             |
    | and product overview.                     |
    | Page 3: The manual covers assembly,       |
    | initial setup, and programming the clock. |
    +-------------------------------------------+
    ```

6.  In the query editor, run the following query to generate multiple responses from a Gemini model based on the analysis of an array of `  ObjectRef  ` values:
    
    ``` text
    WITH
      input_chunked_objrefs AS (
        SELECT row_id, offset, chunk_ref
        FROM
          (
            SELECT ROW_NUMBER() OVER () AS row_id, * FROM `cymbal_pets.map_manual_to_chunks`
          ) AS indexed_table
        LEFT JOIN
          UNNEST(indexed_table.chunks) AS chunk_ref
          WITH OFFSET
      ),
      get_access_urls AS (
        SELECT row_id, offset, chunk_ref, OBJ.GET_ACCESS_URL(chunk_ref, 'r') AS ObjectRefRuntime
        FROM input_chunked_objrefs
      ),
      valid_get_access_urls AS (
        SELECT *
        FROM get_access_urls
        WHERE ObjectRefRuntime['runtime_errors'] IS NULL
      ),
      ordered_output_objrefruntime_array AS (
        SELECT ARRAY_AGG(ObjectRefRuntime ORDER BY offset) AS ObjectRefRuntimeArray
        FROM valid_get_access_urls
        GROUP BY row_id
      )
    SELECT
      page1_summary,
      page2_summary,
      page3_summary
    FROM
      AI.GENERATE_TABLE(
        MODEL `cymbal_pets.gemini`,
        (
          SELECT
            (
              'Can you provide a page by page summary for the first 3 pages of the attached manual? Only write one line for each page. The pages are provided in serial order',
              ObjectRefRuntimeArray) AS prompt,
          FROM ordered_output_objrefruntime_array
        ),
        STRUCT(
          'page1_summary STRING, page2_summary STRING, page3_summary STRING' AS output_schema));
    ```
    
    The results look similar to the following:
    
    ``` console
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

**Caution** : Deleting a project has the following effects:

  - **Everything in the project is deleted.** If you used an existing project for the tasks in this document, when you delete it, you also delete any other work you've done in the project.
  - **Custom project IDs are lost.** When you created this project, you might have created a custom project ID that you want to use in the future. To preserve the URLs that use the project ID, such as an `  appspot.com  ` URL, delete selected resources inside the project instead of deleting the whole project.

If you plan to explore multiple architectures, tutorials, or quickstarts, reusing projects can help you avoid exceeding project quota limits.

In the Google Cloud console, go to the **Manage resources** page.

In the project list, select the project that you want to delete, and then click **Delete** .

In the dialog, type the project ID, and then click **Shut down** to delete the project.
