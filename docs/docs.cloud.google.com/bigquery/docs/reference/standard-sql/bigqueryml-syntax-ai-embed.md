---
name: documents/docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-embed
uri: https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-embed
title: The AI.EMBED function
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

# The AI.EMBED function

This document describes the `AI.EMBED` function, which lets you create [embeddings](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-embed#embeddings) from text or image data in BigQuery. For example, the following query creates an embedding for a piece of text:

The function works by sending a request to a [stable Gemini Enterprise Agent Platform embedding model](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/learn/model-versions#latest-stable) or a [built-in embedding model](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-embed#choose_a_model) in BigQuery, and then returning that model's response.

```
SELECT AI.EMBED("Some text to embed!", endpoint => 'text-embedding-005');
```

## Embeddings

Embeddings are high-dimensional numerical vectors that represent a given entity. Machine learning (ML) models use embeddings to encode semantics about entities to make it easier to reason about and compare them. If two entities are semantically similar, then their respective embeddings are located near each other in the embedding vector space.

Embeddings help you perform the following tasks:

- **Semantic search** : search entities ranked by semantic similarity.
- **Recommendation** : return entities with attributes similar to a given entity.
- **Classification** : return the class of entities whose attributes are similar to the given entity.
- **Clustering** : cluster entities whose attributes are similar to a given entity.
- **Outlier detection** : return entities whose attributes are least related to the given entity.

## Input

Using the `AI.EMBED` function, you can use the following types of input:

- Text data.
- [`ObjectRef` values](https://docs.cloud.google.com/bigquery/docs/work-with-objectref) . You can create an `ObjectRef` value by passing a Cloud Storage URI to the [`OBJ.MAKE_REF` function](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/objectref_functions#objmake_ref) or using an `ObjectRef` column from a table.
- Combinations of unstructured data, including text, images, audio, video, and PDFs, represented by a `STRUCT` that contains `STRING` , `ARRAY<STRING>` , `ObjectRef` , and `ARRAY<ObjectRef>` values.

When you analyze image data, the content must be in one of the supported image formats that are described in the Gemini API model [`mimeType` parameter](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/model-reference/gemini#parameters) .

## Syntax

### Text embedding

```
AI.EMBED(
  [ content => ] 'content',
  { endpoint => 'endpoint' | model => 'model' }
  [, task_type => 'task_type']
  [, title => 'title']
  [, model_params => model_params]
  [, connection_id => 'connection']
)
```

### Arguments

`AI.EMBED` takes the following arguments:

- `content` : a `STRING` value that provides the text or code to embed.

  The `content` value can be a string literal, the name of a table column, or the output of an expression that evaluates to a string.

- `endpoint` : a `STRING` value that specifies a supported Gemini Enterprise Agent Platform [text embedding model](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/text-embeddings-api) endpoint to use. The function incurs charges in Agent Platform each time it's called.

  Different embedding models are generally mathematically incompatible. For information about model retirement dates and how to migrate to a replacement model, see [Handle embedding model deprecation](https://docs.cloud.google.com/bigquery/docs/vector-search-intro#handle-model-deprecation) .

  The endpoint value that you specify must include the model version, for example, `gemini-embedding-001` . If you specify the model name rather than a URL, BigQuery automatically identifies the model and uses the model's full endpoint. For more information, see [Choose a model](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-embed#choose_a_model) .

  The `gemini-embedding-2` model is only available in multi-regional or global endpoints. If you specify the short endpoint name `gemini-embedding-2` , then BigQuery selects an endpoint according to the following rules:

  - If your query is run in the `us` region, or any single region in the US, then BigQuery uses the `us` endpoint.
  - If your query is run in the `eu` region, or any single region in the EU other than `europe-west2` or `europe-west6` , then BigQuery uses the `eu` endpoint.
  - For all other locations, including `europe-west2` and `europe-west6` , BigQuery uses the `global` endpoint.

  To specify a specific endpoint, use a fully qualified multi-regional endpoint name in one of the following formats:

  - `https:// `**`aiplatform.us.rep.googleapis.com`**` /v1/projects/ `` PROJECT_ID `` /locations/ `**`us`**` /publishers/google/models/gemini-embedding-2`
  - `https:// `**`aiplatform.eu.rep.googleapis.com`**` /v1/projects/ `` PROJECT_ID `` /locations/ `**`eu`**` /publishers/google/models/gemini-embedding-2`
  - `https:// `**`aiplatform.googleapis.com`**` /v1/projects/ `` PROJECT_ID `` /locations/ `**`global`**` /publishers/google/models/gemini-embedding-2`

- `model` ( [Preview](https://cloud.google.com/products#product-launch-stages) ): a `STRING` value that specifies a built-in embedding model. Supported values include the following:

  - [`embeddinggemma-2`](https://ai.google.dev/gemma/docs/embeddinggemma/model_card_2)
  - [`embeddinggemma-300m`](https://ai.google.dev/gemma/docs/embeddinggemma/model_card)

  For more information, see [Choose a model](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-embed#choose_a_model) . To request support or provide feedback for these models, send an email to <bqml-feedback@google.com> .

  If you specify `model` , then you can't specify the `endpoint` , `title` , `model_params` , or `connection_id` arguments. If you specify `model => 'embeddinggemma-2'` , then you also can't specify `task_type` .

  Embeddings are generated directly in BigQuery; no data is sent to Agent Platform and no charges are incurred in Agent Platform. For more information, see [Billing and permissions](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-embed#billing_and_permissions) .

- `task_type` : a `STRING` literal that specifies the intended downstream application to help the model produce better quality embeddings. The `task_type` argument accepts the following values:
  - `RETRIEVAL_QUERY` : specifies that the given text is a query in a search or retrieval setting.
  - `RETRIEVAL_DOCUMENT` : specifies that the given text is a document in a search or retrieval setting.
  - `SEMANTIC_SIMILARITY` : specifies that the given text will be used for Semantic Textual Similarity (STS).
  - `CLASSIFICATION` : specifies that the embeddings will be used for classification.
  - `CLUSTERING` : specifies that the embeddings will be used for clustering.
  - `QUESTION_ANSWERING` : specifies that the embeddings will be used for question answering.
  - `FACT_VERIFICATION` : specifies that the embeddings will be used for fact verification.
  - `CODE_RETRIEVAL_QUERY` : specifies that the embeddings will be used for code retrieval.

  Not compatible with the `gemini-embedding-2` model endpoint. Must be `NULL` or omitted when used with the `embeddinggemma-2` built-in model.

- `title` : A `STRING` value that specifies the document title, which the model uses to improve embedding quality. You can only use this parameter if you specify `RETRIEVAL_DOCUMENT` for the `task_type` value. Not compatible with the `gemini-embedding-2` model endpoint.

- `model_params` : a `JSON` literal that provides additional parameters to the model. You can use any of the [`parameters` object](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/model-reference/text-embeddings-api#parameter-list) fields. One of these fields, `outputDimensionality` , lets you specify the number of dimensions to use when generating embeddings. For example, if you specify `256` for the `outputDimensionality` field, then the model returns a 256-dimensional embedding for each input value.

- `connection_id` : a `STRING` value specifying the connection to use to communicate with the model, in the format `PROJECT_ID` . `LOCATION` . `CONNECTION_ID` . For example, `myproject.us.myconnection` .

  For user-initiated queries, the `CONNECTION` argument is optional. When a user initiates a query, BigQuery ML uses the credentials of the user who submitted the query to run it.

  If your query job is expected to run for 48 hours or longer, you should use the `CONNECTION` argument to run the query using a service account.

  Replace the following:

  - ` ``PROJECT_ID`` ` : the project ID of the project that contains the connection.

  - ` ``LOCATION`` ` : the [location](https://docs.cloud.google.com/bigquery/docs/locations) used by the connection. The connection must be in the same region in which the query is run.

  - ` ``CONNECTION_ID`` ` : the connection ID—for example, `myconnection` .

    You can get this value by [viewing the connection details](https://docs.cloud.google.com/bigquery/docs/working-with-connections#view-connections) in the Google Cloud console and copying the value in the last section of the fully qualified connection ID that is shown in **Connection ID** . For example, `projects/myproject/locations/connection_location/connections/ `*`myconnection`* .

  You need to grant the [Agent Platform User role](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control#aiplatform.user) to the connection's service account in the project where you run the function.

### Multimodal embedding

```
AI.EMBED(
  [ content => ] 'content',
  endpoint => 'endpoint'
  [, connection_id => 'connection']
  [, model_params => model_params]
)
```

### Arguments

`AI.EMBED` takes the following arguments:

- `content` : a `STRING` or `ObjectRef` value that provides the data to embed.

  - For text embeddings, you can specify one of the following:
    - A string literal.
    - The name of a `STRING` column.
    - The output of an expression that evaluates to a string.
  - For image content embeddings, you can specify one of the following:
    - The name of an `ObjectRef` column.
    - An [`ObjectRef`](https://docs.cloud.google.com/bigquery/docs/work-with-objectref) value.
  - If you use the `gemini-embedding-2` model, you can also specify a `STRUCT` that contains a combination of `STRING` , `ARRAY<STRING>` , `ObjectRef` , and `ARRAY<ObjectRef>` values.

  `ObjectRef` values must have the `details.gcs_metadata.content_type` elements of the JSON value populated.

- `connection_id` : a `STRING` value specifying the connection to use to communicate with the model, in the format `PROJECT_ID` . `LOCATION` . `CONNECTION_ID` . For example, `myproject.us.myconnection` .

  Replace the following:

  - ` ``PROJECT_ID`` ` : the project ID of the project that contains the connection.

  - ` ``LOCATION`` ` : the [location](https://docs.cloud.google.com/bigquery/docs/locations) used by the connection. The connection must be in the same region in which the query is run.

  - ` ``CONNECTION_ID`` ` : the connection ID—for example, `myconnection` .

    You can get this value by [viewing the connection details](https://docs.cloud.google.com/bigquery/docs/working-with-connections#view-connections) in the Google Cloud console and copying the value in the last section of the fully qualified connection ID that is shown in **Connection ID** . For example, `projects/myproject/locations/connection_location/connections/ `*`myconnection`* .

  You need to grant the [Agent Platform User role](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control#aiplatform.user) to the connection's service account in the project where you run the function.

- `endpoint` : a `STRING` value that specifies a supported Agent Platform [multimodal embedding model](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/model-reference/multimodal-embeddings-api) endpoint to use for the multimodal embedding model.

  Different embedding models are generally mathematically incompatible. For information about model retirement dates and how to migrate to a replacement model, see [Handle embedding model deprecation](https://docs.cloud.google.com/bigquery/docs/vector-search-intro#handle-model-deprecation) .

  The endpoint value that you specify must include the model version, for example `gemini-embedding-2` . If you specify the model name rather than a URL, BigQuery automatically identifies the model and uses the model's full endpoint.

  The `gemini-embedding-2` model is only available in multi-regional or global endpoints. If you specify the short endpoint name `gemini-embedding-2` , then BigQuery selects an endpoint according to the following rules:

  - If your query is run in the `us` region, or any single region in the US, then BigQuery uses the `us` endpoint.
  - If your query is run in the `eu` region, or any single region in the EU other than `europe-west2` or `europe-west6` , then BigQuery uses the `eu` endpoint.
  - For all other locations, including `europe-west2` and `europe-west6` , BigQuery uses the `global` endpoint.

  To specify a specific endpoint, use a fully qualified multi-regional endpoint name in one of the following formats:

  - `https:// `**`aiplatform.us.rep.googleapis.com`**` /v1/projects/ `` PROJECT_ID `` /locations/ `**`us`**` /publishers/google/models/gemini-embedding-2`
  - `https:// `**`aiplatform.eu.rep.googleapis.com`**` /v1/projects/ `` PROJECT_ID `` /locations/ `**`eu`**` /publishers/google/models/gemini-embedding-2`
  - `https:// `**`aiplatform.googleapis.com`**` /v1/projects/ `` PROJECT_ID `` /locations/ `**`global`**` /publishers/google/models/gemini-embedding-2`

- `model_params` : a `JSON` literal that provides additional parameters to the model. Only the `dimension` field is supported. You can use the `dimension` field to specify the number of dimensions to use when generating embeddings. For example, if you specify `256` for the `dimension` field, then the model returns a 256-dimensional embedding for each input value. For more information, see how to [specify lower-dimensional embeddings](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/embeddings/get-multimodal-embeddings#low-dimension) .

## Output

`AI.EMBED` returns a `STRUCT` value for each row in the table. The struct contains the following fields:

- `result` : an `ARRAY<FLOAT64>` value that contains the generated embeddings, or `NULL` if embedding generation fails.
- `status` : a `STRING` value that contains the status for the corresponding row. This value is empty if the operation was successful, or contains an error message if embedding generation fails.

## Examples

### text embedding

The following example shows how to embed a string literal using an Agent Platform endpoint:

```
SELECT
  AI.EMBED(
    'A piece of text to embed',
    endpoint => 'text-embedding-005') AS embedding;
```

The result is similar to the following:

```
+-----------------------+------------------+
| embedding.result      | embedding.status |
+-----------------------+------------------+
| 0.11416172981262207   |                  |
| 0.0041960999369621277 |                  |
| ...                   |                  |
+-----------------------+------------------+
```

The `embedding.result` column contains a single row with an array of length 768. The `embedding.status` column contains an empty string, which indicates that the embedding was successful.

Alternatively, you can perform the embedding by using a built-in embedding model in BigQuery:

```
SELECT
  AI.EMBED(
    'A piece of text to embed',
    model => 'embeddinggemma-2') AS embedding;
```

If you need to reuse embeddings of the same data across many queries, you should save the results to table. The following example generates 768-dimensional embeddings for publicly available BBC news articles and writes the results to a table:

```
CREATE OR REPLACE TABLE mydataset.bbc_news_embeddings AS
SELECT
  title,
  body,
  AI.EMBED(
    body,
    endpoint => 'text-embedding-005',
    model_params => JSON '{"outputDimensionality": 768}'
  ).result AS embedding
FROM
  `bigquery-public-data.bbc_news.fulltext`;
```

The following example queries the table that you just created for the five articles that are most related to the topic "latest news in tech". It calls the `VECTOR_SEARCH` function and uses `AI.EMBED` to create an embedding to pass to the function as the search query.

```
SELECT base.title, base.body
FROM
  VECTOR_SEARCH(
    TABLE mydataset.bbc_news_embeddings,
    # The name of the column that contains the embedding
    'embedding',
    # The embedding to search
    (SELECT AI.EMBED('latest news in tech', endpoint => 'text-embedding-005').result),
    top_k => 5);
```

### multimodal embedding

The following query creates an external table from images of pet products stored in a publicly available Cloud Storage bucket. Then, it generates embeddings for two of the images:

```
# Create a dataset
CREATE SCHEMA IF NOT EXISTS cymbal_pets;

# Create an object table
CREATE OR REPLACE EXTERNAL TABLE cymbal_pets.product_images
WITH CONNECTION DEFAULT
OPTIONS (
  object_metadata = 'SIMPLE',
  uris = ['gs://cloud-samples-data/bigquery/tutorials/cymbal-pets/images/*.png']
);

SELECT
  ref.uri,
  OBJ.GET_READ_URL(ref).url AS signed_url,
  AI.EMBED(
    ref,
    endpoint => 'gemini-embedding-2') AS embedding
FROM
  `cymbal_pets.product_images`
LIMIT 2;
```

The following query uses the `gemini-embedding-2` model to embed the combination of a text description and an image:

```
SELECT
  AI.EMBED(
    ('Made of tempered glass',
    OBJ.MAKE_REF('gs://cloud-samples-data/bigquery/tutorials/cymbal-pets/images/aquaclear-20-gallon-aquarium.png')),
    endpoint => 'gemini-embedding-2');
```

## Choose a model

Use the following table to help you choose an embedding model for your data:

| Model specification                             | Output dimension | Max sequence length | Supported text languages                                                                                                                            | Description                                                                                                                                 | Embedding location      | Billing and permissions                                                                                                                             |
|-------------------------------------------------|------------------|---------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------|-------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------|
| `model => 'embeddinggemma-2'`                   | 768              | 8,192 tokens        | [Supported text languages](https://ai.google.dev/gemma/docs/embeddinggemma)                                                                         | Best for embedding long text and code strings. Specialized for multilingual and coding tasks.                                               | BigQuery                | Incurs charges for model input tokens, plus standard BigQuery query compute charges (slots or bytes processed). No Agent Platform charges or setup. |
| `model => 'embeddinggemma-300m'`                | 768              | 2048 tokens         | [Supported text languages](https://ai.google.dev/gemma/docs/embeddinggemma)                                                                         | Best for embedding short strings (\<= 128 tokens). Specialized for multilingual tasks.                                                      | BigQuery                | Uses and scales with BigQuery slots. No Agent Platform charges or setup.                                                                            |
| `endpoint => 'gemini-embedding-001'`            | up to 3072       | 2048 tokens         | [Supported text languages](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/model-reference/text-embeddings-api#supported_text_languages) | Best performance for multilingual and coding tasks.                                                                                         | Agent Platform endpoint | Incurs Agent Platform charges. Might require Agent Platform permission setup depending on your project settings.                                    |
| `endpoint => 'text-embedding-005'`              | up to 768        | 2048 tokens         | English                                                                                                                                             | Best for embedding long English strings. Specialized in English and coding tasks.                                                           | Agent Platform endpoint | Incurs Agent Platform charges. Might require Agent Platform permission setup depending on your project settings.                                    |
| `endpoint => 'text-multilingual-embedding-002'` | up to 768        | 2048 tokens         | [Supported text languages](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/model-reference/text-embeddings-api#supported_text_languages) | Best for embedding long strings. Specialized in multilingual tasks.                                                                         | Agent Platform endpoint | Incurs Agent Platform charges. Might require Agent Platform permission setup depending on your project settings.                                    |
| `endpoint => 'gemini-embedding-2'`              | up to 3072       | 8192 tokens         | [Supported text languages](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/models#expandable-4)                                          | Best for embedding long strings, including multilingual and unstructured data. Supports a mix of text, images, audio, video, and PDF files. | Agent Platform endpoint | Incurs Agent Platform charges. Might require Agent Platform permission setup depending on your project settings.                                    |

## Billing and permissions

Billing and required permissions depend on whether you specify a built-in model with the `model` argument or a remote model with the `endpoint` argument.

### Billing model

When you specify a `model` value, BigQuery uses a built-in model and doesn't incur charges in Agent Platform. For rates, see [BigQuery ML pricing](https://cloud.google.com/bigquery/pricing#bigquery-ml-pricing) .

- `embeddinggemma-300m` : billed only for BigQuery compute, based on slots used or bytes processed.
- `embeddinggemma-2` : billed to the project in which the query runs for two components:
  - **Model input tokens** : input tokens processed by `embeddinggemma-2` . Output embeddings aren't billed. `NULL` values, empty strings ( `""` ), and input tokens truncated past 8,192 tokens aren't billed. To view billed input tokens, see [Cloud Billing reports](https://docs.cloud.google.com/billing/docs/how-to/reports) for BigQuery. For more information, read about EmbeddingGemma 2 on the [BigQuery pricing page](https://cloud.google.com/bigquery/pricing#embeddinggemma-2-on-bigquery) .
  - **BigQuery compute** : slots used or bytes processed for the rest of the query under your on-demand or editions pricing model.

When you specify an `endpoint` value, the following table describes which project is billed for Agent Platform usage based on the `endpoint` format and the context:

| Endpoint format                                                                                                             | Context                             | Billed project                                 |
|-----------------------------------------------------------------------------------------------------------------------------|-------------------------------------|------------------------------------------------|
| Full path URL. For example, `projects/ `` PROJECT_ID `` /locations/us-central1/publishers/google/models/text-embedding-005` | Standard query or search query      | The project ID specified in the full path URL. |
| Full path URL. For example, `projects/ `` PROJECT_ID `` /locations/us-central1/publishers/google/models/text-embedding-005` | Autonomous embedding background job | The project ID specified in the full path URL. |
| Model name only. For example, `text-embedding-005`                                                                          | Standard query or search query      | The project ID in which the query is run.      |
| Model name only. For example, `text-embedding-005`                                                                          | Autonomous embedding background job | The project ID that contains the table.        |

### Permissions

If you specify a built-in `model` value, you need the `bigquery.jobs.create` permission on the project that runs the query and the `bigquery.tables.getData` permission on the source tables. No Cloud resource connection or Agent Platform role is required.

If you specify an `endpoint` value, the connection used by the `AI.EMBED` function must have the Agent Platform User ( `roles/aiplatform.user` ) role in the project that is billed for Agent Platform usage:

- If you specify a full path for the endpoint, the connection must have permissions in the project specified in that path.
- If you specify only a model name:
  - For standard queries or search queries, the connection must have permissions in the project in which the query is run.
  - For autonomous embedding background jobs, the connection must have permissions in the project that contains the table.

## Locations

If you specify an `endpoint` value, you can run `AI.EMBED` in all of the [locations](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/learn/locations) that support Agent Platform embedding models, and also in the `us` and `eu` multi-regions.

If you specify `model => 'embeddinggemma-2'` , then the following data residency rules apply:

- If you run the query in the `us` multi-region or any single region in the US, then data is processed in the US.
- If you run the query in the `eu` multi-region or any single region in the EU other than `europe-west2` or `europe-west6` , then data is processed in the EU.
- For all other locations, including `europe-west2` and `europe-west6` , there is no data residency commitment and data might be processed outside your query region.

## Quotas

See [generative AI functions quotas and limits](https://docs.cloud.google.com/bigquery/quotas#generative_ai_functions) .

## Limitations

The `embeddinggemma-2` built-in model has the following limitations:

- Embeddings generated by `embeddinggemma-2` can vary slightly across repeated runs, with a cosine distance of up to `1e-4` . Compare vectors using distance thresholds rather than exact floating-point equality.
- The `embeddinggemma-2` model isn't available in Assured Workloads projects. Use `model => 'embeddinggemma-300m'` in these projects instead.

## What's next

- For more information about using Agent Platform models to generate text and embeddings, see [Generative AI overview](https://docs.cloud.google.com/bigquery/docs/generative-ai-overview) .
- For more information about using Cloud AI APIs to perform AI tasks, see [AI application overview](https://docs.cloud.google.com/bigquery/docs/ai-application-overview) .
