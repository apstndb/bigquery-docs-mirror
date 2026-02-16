# Analyze multimodal data in BigQuery

**Preview**

This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

**Note:** To provide feedback or request support for this feature, send an email to <bq-objectref-feedback@google.com> .

This document describes the BigQuery features that you can use to analyze multimodal data. Some features are available in the Google Cloud console and the bq command-line tool, and others are available by using [BigQuery DataFrames](/bigquery/docs/bigquery-dataframes-introduction) in Python. You can use many of these features together to enable easier analysis and transformation workflows for multimodal data.

BigQuery's multimodal data features let you perform the following tasks:

  - Integrate unstructured data into standard tables by using [`  ObjectRef  `](#objectref_values) values.
  - Work with unstructured data in analysis and transformation workflows by using [`  ObjectRefRuntime  `](#objectrefruntime_values) values.
  - Generate text, embeddings, and scalar values from multimodal data by using BigQuery ML [generative AI functions](#generative_ai_functions) with Gemini models.
  - [Create multimodal DataFrames](#multimodal_dataframes) in BigQuery DataFrames.
  - [Transform images and chunk PDF files](#object_transformation_methods) by using BigQuery DataFrames `  Series.BlobAccessor  ` methods.
  - Generate text and embeddings from multimodal data by using BigQuery DataFrames [generative AI methods](#generative_ai_methods) .

For a step-by-step tutorial that uses the Google Cloud console, see [Analyze multimodal data with SQL](/bigquery/docs/multimodal-data-sql-tutorial) . For a step-by-step tutorial that uses BigQuery DataFrames in Python, see [Analyze multimodal data in Python with BigQuery DataFrames](/bigquery/docs/multimodal-data-dataframes-tutorial) .

## Benefits

BigQuery's multimodal data features offer the following benefits:

  - **Composability** : you can store and manage structured and unstructured data in the same standard table row by using `  ObjectRef  ` values. For example, you could store images for a product in the same row as the rest of the product information. You can use standard SQL functions to create and update columns that contain `  ObjectRef  ` values, and you can create `  ObjectRef  ` values as the output of a transformation action on an object.
  - **Using object data in generative AI prompts** : use `  ObjectRefRuntime  ` values as input to generative AI functions. For example, you can generate embeddings on image and text data from the same table. For text and scalar value generation, you can also refer to multiple objects within the prompt you send to a model. For example, you could create a prompt that asks the model to compare two images of animals, and then return text indicating whether they show the same type of animal.
  - **Persisting chunk ordering** : you can chunk objects and then store the chunks as an array of `  ObjectRef  ` values in a standard table column, in order to persist their order. For example, you could parse images from a video, and then store these images as an array of `  ObjectRef  ` values, so that the images stay in the same order that they appear in the original video.

## `     ObjectRef    ` values

An `  ObjectRef  ` value is a `  STRUCT  ` value that uses the [`  ObjectRef  ` format](/bigquery/docs/reference/standard-sql/objectref_functions#objectref) . You can store Cloud Storage object metadata and an associated authorizer in a [BigQuery standard table](/bigquery/docs/tables-intro#standard-tables) by creating a `  STRUCT  ` or `  ARRAY<STRUCT>  ` column that uses this format. The authorizer value identifies the [Cloud resource connection](/bigquery/docs/create-cloud-resource-connection) that BigQuery uses to access the Cloud Storage object.

Use `  ObjectRef  ` values when you need to integrate unstructured data into a standard table. For example, in a products table, you could store product images in the same row with the rest of the product information by adding a column containing an `  ObjectRef  ` value.

Create and update `  ObjectRef  ` values by using the following GoogleSQL functions:

  - [`  OBJ.MAKE_REF  `](/bigquery/docs/reference/standard-sql/objectref_functions#objmake_ref) : create an `  ObjectRef  ` value that contains metadata for a Cloud Storage object.
  - [`  OBJ.FETCH_METADATA  `](/bigquery/docs/reference/standard-sql/objectref_functions#objfetch_metadata) : fetch Cloud Storage metadata for an `  ObjectRef  ` value that is partially populated with `  uri  ` and `  authorizer  ` values.

For more information, see [Specify `  ObjectRef  ` columns in table schemas](/bigquery/docs/objectref-columns) .

## `     ObjectRefRuntime    ` values

An `  ObjectRefRuntime  ` value is a `  JSON  ` value that uses the [`  ObjectRefRuntime  ` schema](/bigquery/docs/reference/standard-sql/objectref_functions#objectrefruntime) . An `  ObjectRefRuntime  ` value contains the Cloud Storage object metadata from the `  ObjectRef  ` value that was used to create it, an associated authorizer, and access URLs. You can use the access URLs to read or modify the object in Cloud Storage.

Use `  ObjectRefRuntime  ` values to work with object data in analysis and transformation workflows. The access URLs in `  ObjectRefRuntime  ` values expire after 6 hours at most, although you can configure shorter expiration time. If you persist `  ObjectRefRuntime  ` values anywhere as part of your workflow, you should refresh this data regularly. To persist object metadata, store `  ObjectRef  ` values instead, and then use them to generate `  ObjectRefRuntime  ` values when you need them. `  ObjectRef  ` values don't need to be refreshed unless the underlying objects in Cloud Storage are modified.

Create `  ObjectRefRuntime  ` values by using the [`  OBJ.GET_ACCESS_URL  ` function](/bigquery/docs/reference/standard-sql/objectref_functions#objget_access_url) .

## Generative AI functions

Generate text, embeddings, and scalar values based on `  ObjectRefRuntime  ` input by using the following generative AI functions with Gemini models:

  - [`  AI.GENERATE  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-generate)
  - [`  AI.GENERATE_TEXT  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-generate-text)
  - [`  AI.GENERATE_TABLE  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-generate-table)
  - [`  AI.GENERATE_BOOL  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-generate-bool)
  - [`  AI.GENERATE_DOUBLE  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-generate-double)
  - [`  AI.GENERATE_INT  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-generate-int)
  - [`  AI.GENERATE_EMBEDDING  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-generate-embedding)
  - [`  AI.EMBED  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-embed)
  - [`  AI.SIMILARITY  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-similarity)

## Work with multimodal data in Python

You can analyze multimodal data in Python by using BigQuery DataFrames classes and methods.

### Multimodal DataFrames

Create a multimodal DataFrame that integrates structured and unstructured data by using the following [`  Session  `](/python/docs/reference/bigframes/latest/bigframes.session.Session) methods:

  - [`  from_glob_path  ` method](/python/docs/reference/bigframes/latest/bigframes.session.Session#bigframes_session_Session_from_glob_path) : create a multimodal DataFrame from a Cloud Storage bucket.
  - [`  read_gbq_object_table  ` method](/python/docs/reference/bigframes/latest/bigframes.session.Session#bigframes_session_Session_read_gbq_object_table) : create a multimodal DataFrame from an object table.

### Object transformation methods

Transform object data by using the following [`  Series.BlobAccessor  `](/python/docs/reference/bigframes/latest/bigframes.operations.blob.BlobAccessor) methods:

  - [`  pdf_chunk  ` method](/python/docs/reference/bigframes/latest/bigframes.operations.blob.BlobAccessor#bigframes_operations_blob_BlobAccessor_pdf_chunk) : chunk PDF objects from a multimodal DataFrame.

  - The following methods to transform image objects from a multimodal DataFrame:
    
      - [`  image_blur  `](/python/docs/reference/bigframes/latest/bigframes.operations.blob.BlobAccessor#bigframes_operations_blob_BlobAccessor_image_blur)
      - [`  image_normalize  `](/python/docs/reference/bigframes/latest/bigframes.operations.blob.BlobAccessor#bigframes_operations_blob_BlobAccessor_image_normalize)
      - [`  image_resize  `](/python/docs/reference/bigframes/latest/bigframes.operations.blob.BlobAccessor#bigframes_operations_blob_BlobAccessor_image_resize)

### Generative AI methods

Use the following methods to perform generative AI tasks on multimodal data:

  - [`  predict  ` method](/python/docs/reference/bigframes/latest/bigframes.ml.llm.GeminiTextGenerator#bigframes_ml_llm_GeminiTextGenerator_predict) of the [`  GeminiTextGenerator  ` class](/python/docs/reference/bigframes/latest/bigframes.ml.llm.GeminiTextGenerator) : generate text based on multimodal data.
  - [`  predict  ` method](/python/docs/reference/bigframes/latest/bigframes.ml.llm.MultimodalEmbeddingGenerator#bigframes_ml_llm_MultimodalEmbeddingGenerator_predict) of the [`  MultimodalEmbeddingGenerator  ` class](/python/docs/reference/bigframes/latest/bigframes.ml.llm.MultimodalEmbeddingGenerator) : generate embeddings based on multimodal data.

## Object tables

If you are on the allowlist for the multimodal data preview, any new [object tables](/bigquery/docs/object-table-introduction) that you create have a `  ref  ` column that contains an `  ObjectRef  ` value for the given object. The connection that is used to create the object table is used to populate the `  authorizer  ` values in the `  ref  ` column. You can use the `  ref  ` column to populate and refresh `  ObjectRef  ` values in standard tables.

## Limitations

The following limitations apply to BigQuery multimodal data features:

  - You must run any query that references `  ObjectRef  ` values in the same project as the table that contains the `  ObjectRef  ` values.
  - You can't have more than 20 connections in the project and region where you are running queries that reference `  ObjectRef  ` or `  ObjectRefRuntime  ` values. For example, if you are running the queries in `  asia-east1  ` in `  myproject  ` , then you can't have more than 20 connections in `  asia-east1  ` in `  myproject  ` .

## Costs

The following costs are applicable when using multimodal data:

  - Storage of object metadata as `  ObjectRef  ` values in standard tables contributes to the BigQuery storage cost for the table.
  - Queries run on `  ObjectRef  ` values incur BigQuery compute costs.
  - New objects that you create from object transformations incur Cloud Storage costs.
  - New data that you create and persist in BigQuery incurs BigQuery storage costs.
  - Use of generative AI functions incurs Vertex AI costs.
  - Use of BigQuery Python UDFs, and of multimodal DataFrames and object transformations methods in BigQuery DataFrames, incurs Python UDF costs.

For more information, see the following pricing pages:

  - [BigQuery pricing](https://cloud.google.com/bigquery/pricing)
  - [BigQuery Python UDFs pricing](/bigquery/docs/user-defined-functions-python#pricing)
  - [Vertex AI pricing](/vertex-ai/generative-ai/pricing)
  - [Cloud Storage pricing](https://cloud.google.com/storage/pricing)

## What's next

  - [Specify `  ObjectRef  ` columns in table schemas](/bigquery/docs/objectref-columns) .
  - [Analyze multimodal data with SQL](/bigquery/docs/multimodal-data-sql-tutorial) .
  - [Analyze multimodal data in Python with BigQuery DataFrames](/bigquery/docs/multimodal-data-dataframes-tutorial) .
  - Learn more about [Generative AI in BigQuery ML](/bigquery/docs/generative-ai-overview) .
  - Learn more about [BigQuery DataFrames](/bigquery/docs/bigquery-dataframes-introduction) .
