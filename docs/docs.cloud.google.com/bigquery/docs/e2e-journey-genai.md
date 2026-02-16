# End-to-end user journeys for generative AI models

This document describes the user journeys for BigQuery ML remote models, including the statements and functions that you can use to work with remote models. BigQuery ML offers the following types of remote models:

  - [Fine-tuned Google Gemini models](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-tuned)
  - [Google, partner, and open models as a service](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model)
  - [Google text embedding models as a service](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-embedding-maas)
  - [Self-deployed open models](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-open)
  - [Cloud AI services](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-service)
  - [Custom models deployed to Vertex AI](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-https)

## Remote model user journeys

The following table describes the statements and functions you can use to create, evaluate, and generate data from remote models:

Model category

Model type

Model creation

[Evaluation](/bigquery/docs/evaluate-overview)

[Inference](/bigquery/docs/inference-overview)

Tutorials

Generative AI remote models

Remote model over a Gemini text generation model <sup>1</sup>

[`  CREATE MODEL  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model)

[`  ML.EVALUATE  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-evaluate)

  - [`  AI.GENERATE_TEXT  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-generate-text)
  - [`  AI.GENERATE_TABLE  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-generate-table)
  - [`  AI.GENERATE  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-generate) <sup>2</sup>
  - [`  AI.GENERATE_BOOL  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-generate-bool) <sup>2</sup>
  - [`  AI.GENERATE_DOUBLE  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-generate-double) <sup>2</sup>
  - [`  AI.GENERATE_INT  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-generate-int) <sup>2</sup>

<!-- end list -->

  - [Generate text using your data](/bigquery/docs/generate-text-tutorial)
  - [Generate structured data using your data](/bigquery/docs/generate-table)
  - [Generate text with Gemini and public data](/bigquery/docs/generate-text-tutorial-gemini)
  - [Handle quota errors by calling `  ML.GENERATE_TEXT  ` iteratively](/bigquery/docs/iterate-generate-text-calls)
  - [Analyze images with a Gemini model](/bigquery/docs/image-analysis)
  - [Try model tuning using public data](/bigquery/docs/tune-evaluate)
  - [Tune a model using your data](/bigquery/docs/generate-text-tuning)

Remote model over a partner text generation model

[`  CREATE MODEL  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model)

[`  ML.EVALUATE  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-evaluate)

[`  AI.GENERATE_TEXT  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-generate-text)

N/A

Remote model over an open text generation model <sup>3</sup>

[`  CREATE MODEL  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-open)

[`  ML.EVALUATE  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-evaluate)

[`  AI.GENERATE_TEXT  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-generate-text)

[Generate text with Gemma and public data](/bigquery/docs/generate-text-tutorial-gemma)

Remote model over a Google embedding generation model

[`  CREATE MODEL  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-embedding-maas)

N/A

[`  AI.GENERATE_EMBEDDING  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-generate-embedding)

  - [Generate text embeddings using your data](/bigquery/docs/generate-text-embedding)
  - [Generate image embeddings using your data](/bigquery/docs/generate-visual-content-embedding)
  - [Generate video embeddings using your data](/bigquery/docs/generate-video-embedding)
  - [Handle quota errors by calling `  ML.GENERATE_EMBEDDING  ` iteratively](/bigquery/docs/iterate-generate-embedding-calls)
  - [Generate and search multimodal embeddings using public data](/bigquery/docs/generate-multimodal-embeddings)

Remote model over an open embedding generation model <sup>3</sup>

[`  CREATE MODEL  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-open)

N/A

[`  AI.GENERATE_EMBEDDING  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-generate-embedding)

[Generate text embeddings by using an open model and the `  AI.GENERATE_EMBEDDING  ` function](/bigquery/docs/generate-text-embedding-tutorial-open-models)

Cloud AI remote models

Remote model over the Cloud Vision API

[`  CREATE MODEL  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-service)

N/A

[`  ML.ANNOTATE_IMAGE  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-annotate-image)

[Annotate images](/bigquery/docs/annotate-image)

Remote model over the Cloud Translation API

[`  CREATE MODEL  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-service)

N/A

[`  ML.TRANSLATE  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-translate)

[Translate text](/bigquery/docs/translate-text)

Remote model over the Cloud Natural Language API

[`  CREATE MODEL  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-service)

N/A

[`  ML.UNDERSTAND_TEXT  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-understand-text)

[Understand text](/bigquery/docs/understand-text)

Remote model over the Document AI API

[`  CREATE MODEL  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-service)

N/A

[`  ML.PROCESS_DOCUMENT  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-process-document)

  - [Process documents](/bigquery/docs/process-document)
  - [Parse PDFs in a RAG pipeline](/bigquery/docs/rag-pipeline-pdf)

Remote model over the Speech-to-Text API

[`  CREATE MODEL  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-service)

N/A

[`  ML.TRANSCRIBE  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-transcribe)

[Transcribe audio files](/bigquery/docs/transcribe)

Remote model over a custom model deployed to Vertex AI

Remote model over a custom model deployed to Vertex AI

[`  CREATE MODEL  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-https)

[`  ML.EVALUATE  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-evaluate)

[`  ML.PREDICT  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-predict)

[Make predictions with a custom model](/bigquery/docs/bigquery-ml-remote-model-tutorial)

<sup>1</sup> Some Gemini models support [supervised tuning](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-tuned#supervised_tuning) .

<sup>2</sup> This function calls a hosted Gemini model, and doesn't require you to create a model separately using the `  CREATE MODEL  ` statement.

<sup>3</sup> You can automatically deploy an open model when you create the BigQuery ML remote model by specifying the model's Hugging Face or Vertex AI Model Garden ID. BigQuery manages the Vertex AI resources of open models deployed in this way, and lets you interact with those Vertex AI resources by using the BigQuery ML `  ALTER MODEL  ` and `  DROP MODEL  ` statements. It also lets you configure automatic undeployment of the model. For more information, see [Automatically deployed models](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-open#automatically_deployed_models) . This feature is in [Preview](https://cloud.google.com/products#product-launch-stages) .
