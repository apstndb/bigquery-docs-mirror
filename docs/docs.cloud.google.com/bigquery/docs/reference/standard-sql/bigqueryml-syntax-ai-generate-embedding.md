# The AI.GENERATE\_EMBEDDING function

This document describes the `  AI.GENERATE_EMBEDDING  ` function, a table-valued function that lets you create embeddings that describe an entity—for example, a piece of text or an image.

Embeddings are high-dimensional numerical vectors that represent a given entity. Machine learning models use embeddings to encode semantics about entities to make it easier to reason about and compare them. If two entities are semantically similar, then their respective embeddings are located near each other in the embedding vector space. For more information, see the [Introduction to embeddings](/bigquery/docs/vector-search-intro) .

You can create embeddings for the following types of data:

  - Text data from standard tables.
  - Visual data that is returned as [`  ObjectRefRuntime  `](/bigquery/docs/reference/standard-sql/objectref_functions#objectrefruntime) values by the [`  OBJ.GET_ACCESS_URL  ` function](/bigquery/docs/reference/standard-sql/objectref_functions#objget_access_url) . You can use [`  ObjectRef  `](/bigquery/docs/reference/standard-sql/objectref_functions#objectref) values from standard tables as input to the `  OBJ.GET_ACCESS_URL  ` function. ( [Preview](https://cloud.google.com/products#product-launch-stages) )
  - Visual data in [object tables](/bigquery/docs/object-table-introduction) .
  - Output data from [PCA](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-pca) , [autoencoder](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-autoencoder) , or [matrix factorization](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-matrix-factorization) models.

## Function processing

Depending on the task, the `  AI.GENERATE_EMBEDDING  ` function works in one of the following ways:

  - To generate embeddings from text or visual content, `  AI.GENERATE_EMBEDDING  ` sends the request to a BigQuery ML [remote model](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model) that represents a [Vertex AI embedding model](/vertex-ai/generative-ai/docs/models#embeddings-models) or a [supported open model](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-open#supported_open_models) ( [Preview](https://cloud.google.com/products#product-launch-stages) ), and then returns the model's response.
    
    The `  AI.GENERATE_EMBEDDING  ` function works with the Vertex AI model to perform embedding tasks supported by that model. For more information on the types of tasks these models can perform, see the following documentation:
    
      - [Text embedding model use cases](/vertex-ai/generative-ai/docs/embeddings#text-use-cases)
      - [Multimodal embedding model use cases](/vertex-ai/generative-ai/docs/embeddings#multimodal-use-cases)
    
    Typically, you want to use text embedding models for text-only use cases, and use multimodal models for cross-modal search use cases, where embeddings for text and visual content are generated in the same semantic space.

  - For PCA and autoencoding, `  AI.GENERATE_EMBEDDING  ` processes the request using a BigQuery ML PCA or autoencoder model [`  ML.PREDICT  ` function](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-predict) . `  AI.GENERATE_EMBEDDING  ` gathers the `  ML.PREDICT  ` output for the model into an array and outputs it as the `  embedding  ` column. Having all of the embeddings in a single column lets you directly use the [`  VECTOR_SEARCH  ` function](/bigquery/docs/reference/standard-sql/search_functions#vector_search) on the `  AI.GENERATE_EMBEDDING  ` output.

  - For matrix factorization, `  AI.GENERATE_EMBEDDING  ` processes the request using a BigQuery ML matrix factorization model and the [`  ML.WEIGHTS  ` function](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-weights) . `  AI.GENERATE_EMBEDDING  ` gathers the `  factor_weights.weight  ` and `  intercept  ` values from the `  ML.WEIGHTS  ` output for the model into an array and outputs it as the `  embedding  ` column. Having all of the embeddings in a single column lets you directly use the [`  VECTOR_SEARCH  ` function](/bigquery/docs/reference/standard-sql/search_functions#vector_search) on the `  AI.GENERATE_EMBEDDING  ` output.

## Syntax

`  AI.GENERATE_EMBEDDING  ` syntax differs depending on the BigQuery ML model you choose. If you use a remote model, it also differs depending on the Vertex AI model that your remote models targets. To understand the differences between the different text embedding models, see [Supported text embedding models](#supported-text-models) .

### Text embedding

``` text
AI.GENERATE_EMBEDDING(
  MODEL `PROJECT_ID.DATASET.MODEL_NAME`,
  { TABLE `PROJECT_ID.DATASET.TABLE_NAME` | (QUERY_STATEMENT) },
  STRUCT(
    [, TASK_TYPE AS task_type]
    [, OUTPUT_DIMENSIONALITY AS output_dimensionality])
)
```

### Arguments

`  AI.GENERATE_EMBEDDING  ` takes the following arguments:

  - `  PROJECT_ID  ` : the project that contains the resource.

  - `  DATASET  ` : the BigQuery dataset that contains the resource.

  - `  MODEL_NAME  ` : the name of a remote model over a [Vertex AI text embedding model](/vertex-ai/generative-ai/docs/embeddings/get-text-embeddings#google-models) .
    
    You can confirm what LLM is used by the remote model by opening the Google Cloud console and looking at the **Remote endpoint** field in the model details page.

  - `  TABLE_NAME  ` : the name of the BigQuery table that contains a `  STRING  ` column to embed. The text in the column that's named `  content  ` is sent to the model. If your table doesn't have a `  content  ` column, use a `  SELECT  ` statement for this argument to provide an alias for an existing table column. An error occurs if no `  content  ` column exists.

  - `  QUERY_STATEMENT  ` : a query whose result contains a `  STRING  ` column that's named `  content  ` . For information about the supported SQL syntax of the `  QUERY_STATEMENT  ` clause, see [GoogleSQL query syntax](/bigquery/docs/reference/standard-sql/query-syntax#sql_syntax) .

  - `  TASK_TYPE  ` : a `  STRING  ` literal that specifies the intended downstream application to help the model produce better quality embeddings. For a list of supported task types and how to choose which one to use, see [Choose an embeddings task type](/vertex-ai/generative-ai/docs/embeddings/task-types) .

  - `  OUTPUT_DIMENSIONALITY  ` : an `  INT64  ` value that specifies the number of dimensions to use when generating embeddings. For example, if you specify `  256 AS output_dimensionality  ` , then the `  embedding  ` output column contains a 256-dimensional embedding for each input value. To find the supported range of output dimensions, read about the available [Google text embedding models](/vertex-ai/generative-ai/docs/embeddings/get-text-embeddings#google-models) .

### Details

The model and input table must be in the same region.

### Open models

**Preview**

This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

**Note:** To give feedback or request support for this feature, contact <bqml-feedback@google.com> .

``` text
AI.GENERATE_EMBEDDING(
  MODEL `PROJECT_ID.DATASET.MODEL_NAME`,
  { TABLE `PROJECT_ID.DATASET.TABLE_NAME` | (QUERY_STATEMENT) }
)
```

### Arguments

`  AI.GENERATE_EMBEDDING  ` takes the following arguments:

  - `  PROJECT_ID  ` : the project that contains the resource.

  - `  DATASET  ` : the BigQuery dataset that contains the resource.

  - `  MODEL_NAME  ` : the name of a remote model over a supported open model.
    
    You can confirm the type of model by opening the Google Cloud console and looking at the **Model type** field in the model details page.

  - `  TABLE_NAME  ` : the name of the BigQuery table that contains a `  STRING  ` column to embed. The text in the column that's named `  content  ` is sent to the model. If your table doesn't have a `  content  ` column, use a `  SELECT  ` statement for this argument to provide an alias for an existing table column. An error occurs if no `  content  ` column exists.

  - `  QUERY_STATEMENT  ` : a query whose result contains a `  STRING  ` column that's named `  content  ` . For information about the supported SQL syntax of the `  QUERY_STATEMENT  ` clause, see [GoogleSQL query syntax](/bigquery/docs/reference/standard-sql/query-syntax#sql_syntax) .

### Details

The model and input table must be in the same region.

### `       multimodalembedding      `

``` text
# Syntax for standard tables
AI.GENERATE_EMBEDDING(
  MODEL `PROJECT_ID.DATASET.MODEL_NAME`,
  { TABLE `PROJECT_ID.DATASET.TABLE_NAME` | (QUERY_STATEMENT) },
  STRUCT(
    [, OUTPUT_DIMENSIONALITY AS output_dimensionality])
)
```

``` text
# Syntax for object tables
AI.GENERATE_EMBEDDING(
  MODEL `PROJECT_ID.DATASET.MODEL_NAME`,
  { TABLE `PROJECT_ID.DATASET.TABLE_NAME` | (QUERY_STATEMENT) },
  STRUCT(
    [, START_SECOND AS start_second]
    [, END_SECOND AS end_second]
    [, INTERVAL_SECONDS AS interval_seconds]
    [, OUTPUT_DIMENSIONALITY AS output_dimensionality])
)
```

### Arguments

`  AI.GENERATE_EMBEDDING  ` takes the following arguments:

  - `  PROJECT_ID  ` : the project that contains the resource.

  - `  DATASET  ` : the BigQuery dataset that contains the resource.

  - `  MODEL_NAME  ` : the name of a remote model over a Vertex AI `  multimodalembedding@001  ` model.
    
    You can confirm what LLM is used by the remote model by opening the Google Cloud console and looking at the **Remote endpoint** field in the model details page.

  - `  TABLE_NAME  ` : one of the following:
    
      - If you are creating embeddings for text in a standard table, the name of the BigQuery table that contains the content. The content must be in a `  STRING  ` column named `  content  ` . If your table does not have a `  content  ` column, use the `  QUERY_STATEMENT  ` argument instead and provide a `  SELECT  ` statement that includes an alias for an existing table column. An error occurs if no `  content  ` column is available.
    
      - If you are creating embeddings for visual content using data from an an object table, the name of a BigQuery [object table](/bigquery/docs/object-table-introduction) that contains the visual content.

  - `  QUERY_STATEMENT  ` : the GoogleSQL query that generates the input data for the function.
    
      - If you are creating embeddings from a standard table, the query must produce a column named `  content  ` , which you can generate as follows:
        
          - For text embeddings, you can pull the value from a `  STRING  ` column, or you can specify a string literal in the query.
        
          - For visual content embeddings, you can provide an [`  ObjectRefRuntime  `](/bigquery/docs/reference/standard-sql/objectref_functions#objectrefruntime) value for the `  content  ` column. You can generate `  ObjectRefRuntime  ` values by using the [`  OBJ.GET_ACCESS_URL  ` function](/bigquery/docs/reference/standard-sql/objectref_functions#objget_access_url) . The `  OBJ.GET_ACCESS_URL  ` function takes an [`  ObjectRef  `](/bigquery/docs/analyze-multimodal-data#objectref_values) value as input, which you can provide by either specifying the name of a column that contains `  ObjectRef  ` values, or by constructing an `  ObjectRef  ` value.
            
            `  ObjectRefRuntime  ` values must have the `  access_url.read_url  ` and `  details.gcs_metadata.content_type  ` elements of the JSON value populated.
    
      - If you are creating embeddings from an object table, the query doesn't have to return a `  content  ` column. You can only specify `  WHERE  ` , `  ORDER BY  ` , and `  LIMIT  ` clauses in the query.

  - `  START_SECOND  ` : a `  FLOAT64  ` value that specifies the second in the video at which to start the embedding. The default value is `  0  ` . If you specify this argument, you must also specify the `  END_SECOND  ` argument. This value must be positive and less than the `  END_SECOND  ` value. This argument only applies to video content.

  - `  END_SECOND  ` : a `  FLOAT64  ` value that specifies the second in the video at which to end the embedding. The `  END_SECOND  ` value can't be higher than `  120  ` . The default value is `  120  ` . If you specify this argument, you must also specify the `  START_SECOND  ` argument. This value must be positive and greater than the `  START_SECOND  ` value. This argument only applies to video content.

  - `  INTERVAL_SECONDS  ` : a `  FLOAT64  ` value that specifies the interval to use when creating embeddings. For example, if you set `  START_SECOND  ` = `  0  ` , `  END_SECOND  ` = `  120  ` , and `  INTERVAL_SECONDS  ` = `  10  ` , then the video is split into twelve 10 second segments ( `  [0, 10), [10, 20), [20, 30)...  ` ) and embeddings are generated for each segment. This value must be greater than or equal to `  4  ` and less than `  120  ` . The default value is `  16  ` . This argument only applies to video content.

  - `  OUTPUT_DIMENSIONALITY  ` : an `  INT64  ` value that specifies the number of dimensions to use when generating embeddings. Valid values are `  128  ` , `  256  ` , `  512  ` , and `  1408  ` . The default value is `  1408  ` . For example, if you specify `  256 AS output_dimensionality  ` , then the `  embedding  ` output column contains a 256-dimensional embedding for each input value.
    
    You can only use this argument when creating text or image embeddings. If you use this argument when creating video embeddings, the function returns an error.

### Details

The model and input table must be in the same region.

### PCA

``` text
AI.GENERATE_EMBEDDING(
  MODEL `PROJECT_ID.DATASET.MODEL_NAME`,
  { TABLE `PROJECT_ID.DATASET.TABLE_NAME` | (QUERY_STATEMENT) }
)
```

### Arguments

`  AI.GENERATE_EMBEDDING  ` takes the following arguments:

  - `  PROJECT_ID  ` : the project that contains the resource.

  - `  DATASET  ` : the BigQuery dataset that contains the resource.

  - `  MODEL_NAME  ` : the name of a PCA model.
    
    You can confirm the type of model by opening the Google Cloud console and looking at the **Model type** field in the model details page.

  - `  TABLE_NAME  ` : the name of the BigQuery table that contains the input data for the PCA model.

  - `  QUERY_STATEMENT  ` : a query whose result contains the input data for the PCA model.

### Details

The model and input table must be in the same region.

### Autoencoder

``` text
AI.GENERATE_EMBEDDING(
  MODEL `PROJECT_ID.DATASET.MODEL_NAME`,
  { TABLE `PROJECT_ID.DATASET.TABLE_NAME` | (QUERY_STATEMENT) },
  STRUCT([TRIAL_ID AS trial_id])
)
```

### Arguments

`  AI.GENERATE_EMBEDDING  ` takes the following arguments:

  - `  PROJECT_ID  ` : the project that contains the resource.

  - `  DATASET  ` : the BigQuery dataset that contains the resource.

  - `  MODEL_NAME  ` : the name of an autoencoder model.
    
    You can confirm the type of model by opening the Google Cloud console and looking at the **Model type** field in the model details page.

  - `  TABLE_NAME  ` : the name of the BigQuery table that contains the input data for the autoencoder model.

  - `  QUERY_STATEMENT  ` : a query whose result contains the input data for the autoencoder model.

  - `  TRIAL_ID  ` : an `  INT64  ` value that identifies the hyperparameter tuning trial that you want the function to evaluate. The function uses the optimal trial by default. Only specify this argument if you ran hyperparameter tuning when creating the model.

### Details

The model and input table must be in the same region.

### Matrix factorization

``` text
AI.GENERATE_EMBEDDING(
  MODEL `PROJECT_ID.DATASET.MODEL_NAME`,
  STRUCT([TRIAL_ID AS trial_id])
)
```

### Arguments

`  AI.GENERATE_EMBEDDING  ` takes the following arguments:

  - `  PROJECT_ID  ` : the project that contains the resource.

  - `  DATASET  ` : the BigQuery dataset that contains the resource.

  - `  MODEL_NAME  ` : the name of a matrix factorization model.
    
    You can confirm the type of model by opening the Google Cloud console and looking at the **Model type** field in the model details page.

  - `  TRIAL_ID  ` : an `  INT64  ` value that identifies the hyperparameter tuning trial that you want the function to evaluate. The function uses the optimal trial by default. Only specify this argument if you ran hyperparameter tuning when creating the model.

## Output

`  AI.GENERATE_EMBEDDING  ` returns the input table and the following columns:

### Text embedding

  - `  embedding  ` : an `  ARRAY<FLOAT64>  ` value that contains the generated embedding vector.
  - `  statistics  ` : a `  JSON  ` value that contains a `  token_count  ` field with the number of tokens in the content, and a `  truncated  ` field that indicates whether the content was truncated.
  - `  status  ` : a `  STRING  ` value that contains the API response status for the corresponding row. This value is empty if the operation was successful.

### Open models

  - `  embedding  ` : an `  ARRAY<FLOAT64>  ` value that contains the generated embedding vector.
  - `  status  ` : a `  STRING  ` value that contains the API response status for the corresponding row. This value is empty if the operation was successful.

### `       multimodalembedding      `

  - `  embedding  ` : an `  ARRAY<FLOAT64>  ` value that contains the generated embedding vector.

  - `  status  ` : a `  STRING  ` value that contains the API response status for the corresponding row. This value is empty if the operation was successful.

  - `  video_start_sec  ` : for video content, an `  INT64  ` value that contains the starting second of the portion of the video that the embedding represents. For image content, the value is `  NULL  ` . This column isn't returned for text content.

  - `  video_end_sec  ` : for video content, an `  INT64  ` value that contains the ending second of the portion of the video that the embedding represents. For image content, the value is `  NULL  ` . This column isn't returned for text content.

### PCA

`  embedding  ` : an `  ARRAY<FLOAT>  ` value that contains the principal components for the input data. The number of array dimensions is equal to the PCA model's [`  NUM_PRINCIPAL_COMPONENTS  ` option](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-pca#num_principal_components) value if that option is used when the model is created. If the [`  PCA_EXPLAINED_VARIANCE_RATIO  ` option](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-pca#pca_explained_variance_ratio) is used instead, the array dimensions vary depending on the input table and the option ratio determined by BigQuery ML.

### Autoencoder

`  embedding  ` : an `  ARRAY<FLOAT>  ` value that contains the latent space dimensions for the input data. The number of array dimensions is equal to the number in the middle of the autoencoder model's [`  HIDDEN_UNITS  ` option](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-autoencoder#hidden_units) array value.

`  trial_id  ` : an `  INT64  ` value that identifies the hyperparameter tuning trial used by the function. This column is only returned if you ran hyperparameter tuning when creating the model.

### Matrix factorization

`  embedding  ` : an `  ARRAY<FLOAT>  ` value that contains the weights of the feature, and also the intercept or bias term for the feature. The intercept value is the last value in the array. The number of array dimensions is equal to the matrix factorization model's [`  NUM_FACTORS  ` option](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-matrix-factorization#num_factors) value.

`  trial_id  ` : an `  INT64  ` value that identifies the hyperparameter tuning trial used by the function. This column is only returned if you ran hyperparameter tuning when creating the model.

`  processed_input  ` : a `  STRING  ` value that contains the name of the user or item column. The value of this column matches the name of the user or item column provided in the [`  query_statement  ` clause](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create#query_statement) that was used when the matrix factorization model was trained.

`  feature  ` : a `  STRING  ` value that contains the names of the specific users or items used during training.

## Examples

### `       text-embedding      `

This example shows how to generate an embedding of a single piece of sample text by using a remote model that references a `  text-embedding  ` model.

Create the remote model:

``` text
CREATE OR REPLACE MODEL `mydataset.text_embedding`
  REMOTE WITH CONNECTION `us.test_connection`
  OPTIONS(ENDPOINT = 'text-embedding-005')
```

Generate the embedding:

``` text
SELECT *
FROM
  AI.GENERATE_EMBEDDING(
    MODEL `mydataset.text_embedding`,
    (SELECT "Example text to embed" AS content)
);
```

The result is similar to the following:

``` text
+-----------------------+-------------------------------------+--------+-----------------------+
| embedding             | statistics                          | status | content               |
+-----------------------+-------------------------------------+--------+-----------------------+
| -0.097711019217967987 | {"token_count":4,"truncated":false} |        | Example text to embed |
|  0.014618906192481518 |                                     |        |                       |
| ...                   |                                     |        |                       |
+-----------------------+-------------------------------------+--------+-----------------------+
```

### `       multimodalembedding      `

This example shows how to generate embeddings from visual content by using a remote model that references a `  multimodalembedding  ` model.

Create the remote model:

``` text
CREATE OR REPLACE MODEL `mydataset.multimodalembedding`
  REMOTE WITH CONNECTION `us.test_connection`
  OPTIONS(ENDPOINT = 'multimodalembedding@001')
```

**Use an `  ObjectRefRuntime  ` value**

Generate embeddings from visual content in an `  ObjectRef  ` column in a standard table:

``` text
SELECT *
FROM AI.GENERATE_EMBEDDING(
  MODEL `mydataset.multimodalembedding`,
    (
      SELECT OBJ.GET_ACCESS_URL(art_image, 'r') as content
      FROM `mydataset.art`)
 );
```

**Use an object table**

Generate embeddings from visual content in an object table:

``` text
SELECT *
FROM AI.GENERATE_EMBEDDING(
  MODEL `mydataset.multimodalembedding`,
  TABLE `mydataset.my_object_table`);
```

### PCA

This example shows how to generate embeddings that represent the principal components of a PCA model.

Create the PCA model:

``` text
CREATE OR REPLACE MODEL `mydataset.pca_nyc_trees`
  OPTIONS (
    MODEL_TYPE = 'PCA',
    PCA_EXPLAINED_VARIANCE_RATIO = 0.9)
AS (
  SELECT
    tree_id,
    block_id,
    tree_dbh,
    stump_diam,
    curb_loc,
    status,
    health,
    spc_latin
  FROM
    `bigquery-public-data.new_york_trees.tree_census_2015`
);
```

Generate embeddings that represent principal components:

``` text
SELECT *
FROM
  AI.GENERATE_EMBEDDING(
    MODEL `mydataset.pca_nyc_trees`,
(
  SELECT
    tree_id,
    block_id,
    tree_dbh,
    stump_diam,
    curb_loc,
    status,
    health,
    spc_latin
  FROM
    `bigquery-public-data.new_york_trees.tree_census_2015`
));
```

### Autoencoder

This example shows how to generate embeddings that represent the latent space dimensions of an autoencoder model.

Create the autoencoder model:

``` text
CREATE OR REPLACE MODEL `mydataset.my_autoencoder_model`
  OPTIONS (
    model_type = 'autoencoder',
    activation_fn = 'relu',
    batch_size = 8,
    dropout = 0.2,
    hidden_units =
      [
        32,
        16,
        4,
        16,
        32],
    learn_rate = 0.001,
    l1_reg_activation = 0.0001,
    max_iterations = 10,
    optimizer = 'adam')
AS
SELECT * EXCEPT (
    Time,
    Class)
FROM
  `bigquery-public-data.ml_datasets.ulb_fraud_detection`;
```

Generate embeddings that represent latent space dimensions:

``` text
SELECT
  *
FROM
  AI.GENERATE_EMBEDDING(
    MODEL `mydataset.my_autoencoder_model`,
    TABLE `bigquery-public-data.ml_datasets.ulb_fraud_detection`);
```

### Matrix factorization

This example shows how to generate embeddings that represent the underlying weights that the matrix factorization model uses during prediction.

Create the matrix factorization model:

``` text
CREATE OR REPLACE MODEL
  `mydataset.my_mf_model`
OPTIONS (
  model_type='matrix_factorization',
  user_col='user_id',
  item_col='item_id',
  l2_reg=9.83,
  num_factors=34)
AS SELECT
  user_id,
  item_id,
  AVG(rating) as rating
FROM
  movielens.movielens_1m
GROUP BY user_id, item_id;
```

Generate embeddings that represent model weights and intercepts:

``` text
SELECT
  *
FROM
  AI.GENERATE_EMBEDDING(MODEL `mydataset.my_mf_model`)
```

## Supported text embedding models

The following tables show the available Google and open text embedding models.

### Google models

You can get text embeddings by using the following models:

<table>
<thead>
<tr class="header">
<th>Model name</th>
<th>Description</th>
<th>Output Dimensions</th>
<th>Max sequence length</th>
<th>Supported text languages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       gemini-embedding-001      </code></td>
<td>State-of-the-art performance across English, multilingual and code tasks. It unifies the previously specialized models like <code dir="ltr" translate="no">       text-embedding-005      </code> and <code dir="ltr" translate="no">       text-multilingual-embedding-002      </code> and achieves better performance in their respective domains. Read our <a href="https://deepmind.google/research/publications/157741/">Tech Report</a> for more detail.</td>
<td>up to 3072</td>
<td>2048 tokens</td>
<td><a href="/vertex-ai/generative-ai/docs/model-reference/text-embeddings-api#supported_text_languages">Supported text languages</a></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       text-embedding-005      </code></td>
<td>Specialized in English and code tasks.</td>
<td>up to 768</td>
<td>2048 tokens</td>
<td>English</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       text-multilingual-embedding-002      </code></td>
<td>Specialized in multilingual tasks.</td>
<td>up to 768</td>
<td>2048 tokens</td>
<td><a href="/vertex-ai/generative-ai/docs/model-reference/text-embeddings-api#supported_text_languages">Supported text languages</a></td>
</tr>
</tbody>
</table>

For superior embedding quality, `  gemini-embedding-001  ` is our large model designed to provide the highest performance.

### Open models

You can get text embeddings by using the following models:

<table>
<thead>
<tr class="header">
<th>Model name</th>
<th>Description</th>
<th>Output dimensions</th>
<th>Max sequence length</th>
<th>Supported text languages</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       multilingual-e5-small      </code></td>
<td>Part of the E5 family of text embedding models. Small variant contains 12 layers.</td>
<td>Up to 384</td>
<td>512 tokens</td>
<td><a href="https://huggingface.co/intfloat/multilingual-e5-small#supported-languages">Supported languages</a></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       multilingual-e5-large      </code></td>
<td>Part of the E5 family of text embedding models. Large variant contains 24 layers.</td>
<td>Up to 1024</td>
<td>512 tokens</td>
<td><a href="https://huggingface.co/intfloat/multilingual-e5-small#supported-languages">Supported languages</a></td>
</tr>
</tbody>
</table>

To get started, see the E5 family [model card](https://console.cloud.google.com/vertex-ai/publishers/intfloat/model-garden/multilingual-e5-large-instruct-maas) . For more information on open models, see [Open models for MaaS](/vertex-ai/generative-ai/docs/maas/use-open-models)

## Supported visual content

You can use the `  AI.GENERATE_EMBEDDING  ` function to generate embeddings for videos and images that meet the requirements described in [API limits](/vertex-ai/generative-ai/docs/embeddings/get-multimodal-embeddings#api-limits) .

There is no limitation on the length of the video files you can use with this function. However, the function only processes the first two minutes of a video. If a video is longer than two minutes, the `  AI.GENERATE_EMBEDDING  ` function only returns embeddings for the first two minutes.

## Known issues

Sometimes after a query job that uses this function finishes successfully, some returned rows contain the following error message:

``` text
A retryable error occurred: RESOURCE EXHAUSTED error from <remote endpoint>
```

This issue occurs because BigQuery query jobs finish successfully even if the function fails for some of the rows. The function fails when the volume of API calls to the remote endpoint exceeds the quota limits for that service. This issue occurs most often when you are running multiple parallel batch queries. BigQuery retries these calls, but if the retries fail, the `  resource exhausted  ` error message is returned.

To iterate through inference calls until all rows are successfully processed, you can use the [BigQuery remote inference SQL scripts](https://github.com/GoogleCloudPlatform/bigquery-ml-utils/tree/master/sql_scripts/remote_inference) or the [BigQuery remote inference pipeline Dataform package](https://github.com/dataform-co/dataform-bqml) .

## Locations

The `  AI.GENERATE_EMBEDDING  ` function must run in the same [region or multi-region](/bigquery/docs/locations) as the model that the function references. For more information on supported regions for embedding models, see [Google model endpoint locations](/vertex-ai/generative-ai/docs/learn/locations#google_model_endpoint_locations) . Embedding models are also available in the `  US  ` multi-region.

## Quotas

Quotas apply when you use the `  AI.GENERATE_EMBEDDING  ` function with remote models. For more information, see [Vertex AI and Cloud AI service functions quotas and limits](/bigquery/quotas#cloud_ai_service_functions) .

For the `  multimodalembedding  ` model, the default requests per minute (RPM) for non- `  EU  ` regions is 600. The default RPM for `  EU  ` regions is 120. However, you can request a quota increase in order to increase throughput.

To increase quota, first request more quota for the Vertex AI `  multimodalembedding  ` model by using the process described in [Manage your quota using the console](/docs/quotas/view-manage#managing_your_quota_console) . When the model quota has been increased, send an email to <bqml-feedback@google.com> and request a quota increase for the `  AI.GENERATE_EMBEDDING  ` function. Include information about the adjusted `  multimodalembedding  ` quota.

## What's next

  - Try creating embeddings:
    
      - [Creating text embeddings](/bigquery/docs/generate-text-embedding)
      - [Creating image embeddings](/bigquery/docs/generate-visual-content-embedding)
      - [Creating video embeddings](/bigquery/docs/generate-video-embedding)

  - For more information about using Vertex AI models to generate text and embeddings, see [Generative AI overview](/bigquery/docs/generative-ai-overview) .

  - Try the [Perform semantic search and retrieval-augmented generation](/bigquery/docs/vector-index-text-search-tutorial) tutorial to learn how to do the following tasks:
    
      - Generate text embeddings.
      - Create a vector index on the embeddings.
      - Perform a vector search with the embeddings to search for similar text.
      - Perform retrieval-augmented generation (RAG) by using vector search results to augment the prompt input and improve results.

  - Try the [Parse PDFs in a retrieval-augmented generation pipeline](/bigquery/docs/rag-pipeline-pdf) tutorial to learn how to create a RAG pipeline based on parsed PDF content.

  - For more information about using Cloud AI APIs to perform AI tasks, see [AI application overview](/bigquery/docs/ai-application-overview) .

  - For more information about supported SQL statements and functions for generative AI models, see [End-to-end user journeys for generative AI models](/bigquery/docs/e2e-journey-genai) .
