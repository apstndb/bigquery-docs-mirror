---
name: documents/docs.cloud.google.com/bigquery/docs/e2e-journey-genai
uri: https://docs.cloud.google.com/bigquery/docs/e2e-journey-genai
title: End-to-end user journeys for generative AI models
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

# End-to-end user journeys for generative AI models

This document describes the user journeys for BigQuery ML remote models, including the statements and functions that you can use to work with remote models. BigQuery ML offers the following types of remote models:

- [Fine-tuned Google Gemini models](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-tuned)
- [Google, partner, and open models as a service](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model)
- [Google text embedding models as a service](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-embedding-maas)
- [Self-deployed open models](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-open)
- [Cloud AI services](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-service)
- [Custom models deployed to Gemini Enterprise Agent Platform](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-https)

## Remote model user journeys

The following table describes the statements and functions you can use to create, evaluate, and generate data from remote models:

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>Model category</th>
<th>Model type</th>
<th>Model creation</th>
<th><a href="https://docs.cloud.google.com/bigquery/docs/evaluate-overview">Evaluation</a></th>
<th><a href="https://docs.cloud.google.com/bigquery/docs/inference-overview">Inference</a></th>
<th>Tutorials</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Generative AI remote models</td>
<td>Remote model over a Gemini text generation model <sup>1</sup></td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model"><code>CREATE MODEL</code></a></td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-evaluate"><code>ML.EVALUATE</code></a></td>
<td><ul>
<li><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-generate-text"><code>AI.GENERATE_TEXT</code></a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-generate-table"><code>AI.GENERATE_TABLE</code></a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-generate"><code>AI.GENERATE</code></a> <sup>2</sup></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-generate-bool"><code>AI.GENERATE_BOOL</code></a> <sup>2</sup></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-generate-double"><code>AI.GENERATE_DOUBLE</code></a> <sup>2</sup></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-generate-int"><code>AI.GENERATE_INT</code></a> <sup>2</sup></li>
</ul></td>
<td><ul>
<li><a href="https://docs.cloud.google.com/bigquery/docs/generate-text-tutorial">Generate text using your data</a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/generate-table">Generate structured data using your data</a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/generate-text-tutorial-gemini">Generate text with Gemini and public data</a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/iterate-generate-text-calls">Handle quota errors by calling <code>ML.GENERATE_TEXT</code> iteratively</a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/image-analysis">Analyze images with a Gemini model</a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/tune-evaluate">Try model tuning using public data</a></li>
</ul></td>
</tr>
<tr class="even">
<td>Remote model over a partner text generation model</td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model"><code>CREATE MODEL</code></a></td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-evaluate"><code>ML.EVALUATE</code></a></td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-generate-text"><code>AI.GENERATE_TEXT</code></a></td>
<td>N/A</td>
<td></td>
</tr>
<tr class="odd">
<td>Remote model over an open text generation model <sup>3</sup></td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-open"><code>CREATE MODEL</code></a></td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-evaluate"><code>ML.EVALUATE</code></a></td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-generate-text"><code>AI.GENERATE_TEXT</code></a></td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/generate-text-tutorial-gemma">Generate text with Gemma and public data</a></td>
<td></td>
</tr>
<tr class="even">
<td>Remote model over a Google embedding generation model</td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-embedding-maas"><code>CREATE MODEL</code></a></td>
<td>N/A</td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-generate-embedding"><code>AI.GENERATE_EMBEDDING</code></a></td>
<td><ul>
<li><a href="https://docs.cloud.google.com/bigquery/docs/generate-text-embedding">Generate text embeddings using your data</a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/generate-visual-content-embedding">Generate image embeddings using your data</a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/generate-video-embedding">Generate video embeddings using your data</a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/iterate-generate-embedding-calls">Handle quota errors by calling <code>ML.GENERATE_EMBEDDING</code> iteratively</a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/generate-multimodal-embeddings">Generate and search multimodal embeddings using public data</a></li>
</ul></td>
<td></td>
</tr>
<tr class="odd">
<td>Remote model over an open embedding generation model <sup>3</sup></td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-open"><code>CREATE MODEL</code></a></td>
<td>N/A</td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-generate-embedding"><code>AI.GENERATE_EMBEDDING</code></a></td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/generate-text-embedding-tutorial-open-models">Generate text embeddings by using an open model and the <code>AI.GENERATE_EMBEDDING</code> function</a></td>
<td></td>
</tr>
<tr class="even">
<td>Cloud AI remote models</td>
<td>Remote model over the Cloud Vision API</td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-service"><code>CREATE MODEL</code></a></td>
<td>N/A</td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-annotate-image"><code>ML.ANNOTATE_IMAGE</code></a></td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/annotate-image">Annotate images</a></td>
</tr>
<tr class="odd">
<td>Remote model over the Cloud Translation API</td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-service"><code>CREATE MODEL</code></a></td>
<td>N/A</td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-translate"><code>ML.TRANSLATE</code></a></td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/translate-text">Translate text</a></td>
<td></td>
</tr>
<tr class="even">
<td>Remote model over the Cloud Natural Language API</td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-service"><code>CREATE MODEL</code></a></td>
<td>N/A</td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-understand-text"><code>ML.UNDERSTAND_TEXT</code></a></td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/understand-text">Understand text</a></td>
<td></td>
</tr>
<tr class="odd">
<td>Remote model over the Document AI API</td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-service"><code>CREATE MODEL</code></a></td>
<td>N/A</td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-process-document"><code>ML.PROCESS_DOCUMENT</code></a></td>
<td><ul>
<li><a href="https://docs.cloud.google.com/bigquery/docs/process-document">Process documents</a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/rag-pipeline-pdf">Parse PDFs in a RAG pipeline</a></li>
</ul></td>
<td></td>
</tr>
<tr class="even">
<td>Remote model over the Speech-to-Text API</td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-service"><code>CREATE MODEL</code></a></td>
<td>N/A</td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-transcribe"><code>ML.TRANSCRIBE</code></a></td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/transcribe">Transcribe audio files</a></td>
<td></td>
</tr>
<tr class="odd">
<td>Remote model over a custom model deployed to Gemini Enterprise Agent Platform</td>
<td>Remote model over a custom model deployed to Gemini Enterprise Agent Platform</td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-https"><code>CREATE MODEL</code></a></td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-evaluate"><code>ML.EVALUATE</code></a></td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-predict"><code>ML.PREDICT</code></a></td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/bigquery-ml-remote-model-tutorial">Make predictions with a custom model</a></td>
</tr>
</tbody>
</table>

<sup>1</sup> Some Gemini models support [supervised tuning](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-tuned#supervised_tuning) .

<sup>2</sup> This function calls a hosted Gemini model, and doesn't require you to create a model separately using the `CREATE MODEL` statement.

<sup>3</sup> You can automatically deploy an open model when you create the BigQuery ML remote model by specifying the model's Hugging Face or Agent Platform Model Garden ID. BigQuery manages the Agent Platform resources of open models deployed in this way, and lets you interact with those Agent Platform resources by using the BigQuery ML `ALTER MODEL` and `DROP MODEL` statements. It also lets you configure automatic undeployment of the model. For more information, see [Automatically deployed models](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-open#automatically_deployed_models) .
