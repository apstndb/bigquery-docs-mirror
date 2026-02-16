# The CREATE MODEL statement for Vertex AI embedding models as MaaS

This document describes the `  CREATE MODEL  ` statement for creating remote models in BigQuery over [embedding models](/vertex-ai/generative-ai/docs/embeddings) in Vertex AI as a model as a service (MaaS) by using SQL. When you use MaaS on Vertex AI, you don't have to provision or manage serving infrastructure for your models. Choose MaaS for rapid development and prototyping, when you want to minimize operational overhead. For more information, see [When to use MaaS](/vertex-ai/generative-ai/docs/open-models/choose-serving-option#when_to_use_maas) .

Alternatively, you can use the Google Cloud console user interface to [create a model by using a UI](/bigquery/docs/create-machine-learning-model-console) ( [Preview](https://cloud.google.com/products#product-launch-stages) ) instead of constructing the SQL statement yourself.

After you create the remote model, you can use one of the following functions to perform generative AI with that model:

  - [`  AI.GENERATE_EMBEDDING  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-generate-embedding)

## `     CREATE MODEL    ` syntax

``` sql
{CREATE MODEL | CREATE MODEL IF NOT EXISTS | CREATE OR REPLACE MODEL}
`project_id.dataset.model_name`
REMOTE WITH CONNECTION {DEFAULT | `project_id.region.connection_id`}
OPTIONS(ENDPOINT = 'vertex_ai_embedding_endpoint');
```

### `     CREATE MODEL    `

Creates and trains a new model in the specified dataset. If the model name exists, `  CREATE MODEL  ` returns an error.

### `     CREATE MODEL IF NOT EXISTS    `

Creates and trains a new model only if the model doesn't exist in the specified dataset.

### `     CREATE OR REPLACE MODEL    `

Creates and trains a model and replaces an existing model with the same name in the specified dataset.

### `     model_name    `

The name of the model you're creating or replacing. The model name must be unique in the dataset: no other model or table can have the same name. The model name must follow the same naming rules as a BigQuery table. A model name can:

  - Contain up to 1,024 characters
  - Contain letters (upper or lower case), numbers, and underscores

`  model_name  ` is case-sensitive.

If you don't have a default project configured, then you must prepend the project ID to the model name in the following format, including backticks:

\`\[PROJECT\_ID\].\[DATASET\].\[MODEL\]\`

For example, \`myproject.mydataset.mymodel\`.

### `     REMOTE WITH CONNECTION    `

**Syntax**

``` text
`[PROJECT_ID].[LOCATION].[CONNECTION_ID]`
```

BigQuery uses a [Cloud resource connection](/bigquery/docs/create-cloud-resource-connection) to interact with the Vertex AI endpoint.

The connection elements are as follows:

  - `  PROJECT_ID  ` : the project ID of the project that contains the connection.

  - `  LOCATION  ` : the [location](/bigquery/docs/locations) used by the connection. The connection must be in the same location as the dataset that contains the model.

  - `  CONNECTION_ID  ` : the connection ID—for example, `  myconnection  ` .
    
    To find your connection ID, [view the connection details](/bigquery/docs/working-with-connections#view-connections) in the Google Cloud console. The connection ID is the value in the last section of the fully qualified connection ID that is shown in **Connection ID** —for example `  projects/myproject/locations/connection_location/connections/ myconnection  ` .
    
    To use a [default connection](/bigquery/docs/default-connections) , specify `  DEFAULT  ` instead of the connection string containing PROJECT\_ID . LOCATION . CONNECTION\_ID .

If you are creating a remote model over a Vertex AI model that uses supervised tuning, you need to grant the [Vertex AI Service Agent role](/vertex-ai/docs/general/access-control#aiplatform.serviceAgent) to the connection's service account in the project where you create the model. Otherwise, you need to grant the [Vertex AI User role](/vertex-ai/docs/general/access-control#aiplatform.user) to the connection's service account in the project where you create the model.

If you are using the remote model to analyze unstructured data from an [object table](/bigquery/docs/object-table-introduction) , you must also grant the [Vertex AI Service Agent role](/vertex-ai/docs/general/access-control#aiplatform.serviceAgent) to the service account of the connection associated with the object table. You can find the object table's connection in the Google Cloud console, on the **Details** pane for the object table.

**Example**

``` text
`myproject.us.my_connection`
```

### `     ENDPOINT    `

**Syntax**

``` text
ENDPOINT = 'vertex_ai_embedding_endpoint'
```

**Description**

The Vertex AI endpoint for the model to use. You can specify the name of the Vertex AI model, for example `  gemini-embedding-001  ` , or you can specify the Vertex AI model's endpoint URL, for example `  https://us-central1-aiplatform.googleapis.com/v1/projects/myproject/locations/us-central1/publishers/google/models/gemini-embedding-001  ` . If you specify the model name, BigQuery ML automatically identifies and uses the full endpoint of the Vertex AI model based on the location of the dataset in which you create the model.

**Arguments**

A `  STRING  ` value that contains the model name of the target Vertex AI embedding model. The following embedding models are supported:

### text embedding models

The following [text embedding models](/vertex-ai/generative-ai/docs/embeddings/get-text-embeddings#supported-models) are supported:

  - `  gemini-embedding-001  ` , which supports both English and multilingual input. ( [Preview](https://cloud.google.com/products#product-launch-stages) )
  - `  text-embedding-004  `
  - `  text-embedding-005  `
  - `  text-multilingual-embedding-002  `

After you create a remote model based on an embedding model, you can use the model with the [`  AI.GENERATE_EMBEDDING  ` function](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-generate-embedding) to generate embeddings from text data in a BigQuery table.

### multimodal embedding models

The `  multimodalembedding@001  ` [embedding model](/vertex-ai/generative-ai/docs/embeddings/get-multimodal-embeddings#supported-models) is supported.

After you create a remote model based on a `  multimodalembedding  ` embedding model, you can use the model with the [`  AI.GENERATE_EMBEDDING  ` function](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-generate-embedding) to generate embeddings from text data in a BigQuery table or from visual content in a BigQuery [object table](/bigquery/docs/object-table-introduction) .

For information that can help you choose between the supported models, see [Model information](/vertex-ai/docs/generative-ai/learn/models) .

## Locations

For information about supported locations, see [Locations for remote models](/bigquery/docs/locations#locations-for-remote-models) .

## Examples

The following examples create BigQuery ML remote models.

### Create a text embedding model

The following example creates a BigQuery ML remote model over the `  text-embedding-005  ` model and uses the default connection:

``` text
CREATE OR REPLACE MODEL mydataset.embedding_005
REMOTE WITH CONNECTION DEFAULT
OPTIONS(ENDPOINT = 'text-embedding-005');
```

## What's next

  - For more information about using Vertex AI models with BigQuery ML, see [Generative AI overview](/bigquery/docs/generative-ai-overview) .
  - Try [generating embeddings from BigQuery data](/bigquery/docs/generate-text-embedding) .
  - Try [generating image embeddings](/bigquery/docs/generate-visual-content-embedding) .
