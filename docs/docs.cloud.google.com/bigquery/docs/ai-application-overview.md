# Task-specific solutions overview

This document describes the artificial intelligence (AI) features that BigQuery ML supports. These features let you develop task-specific solutions in BigQuery ML by using Cloud AI APIs. Supported tasks include the following:

  - [Natural language processing](#natural_language_processing)
  - [Machine translation](#machine_translation)
  - [Audio transcription](#audio_transcription)
  - [Document processing](#document_processing)
  - [Computer vision](#computer_vision)

You access a Cloud AI API to perform one of these functions by creating a [remote model](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-service) in BigQuery ML that represents the API endpoint. Once you have created a remote model over the AI resource that you want to use, you access that resource's capabilities by running a BigQuery ML function against the remote model.

This approach lets you use the capabilities of the underlying API without having to know Python or develop familiarity with API.

## Workflow

You can use [remote models over Vertex AI models](/bigquery/docs/generative-ai-overview) and remote models over Cloud AI services together with BigQuery ML functions in order to accomplish complex data analysis and generative AI tasks.

The following diagram shows some typical workflows where you might use these capabilities together:

## Natural language processing

You can use natural language processing to perform tasks such as classification and sentiment analysis on your data. For example, you could analyze product feedback to estimate whether customers like a particular product.

To perform natural language tasks, you can create a reference to the [Cloud Natural Language API](/natural-language) by creating a remote model and specifying `  CLOUD_AI_NATURAL_LANGUAGE_V1  ` for the `  REMOTE_SERVICE_TYPE  ` value. You can then use the [`  ML.UNDERSTAND_TEXT  ` function](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-understand-text) to interact with that service. `  ML.UNDERSTAND_TEXT  ` works with data in [standard tables](/bigquery/docs/tables-intro#standard-tables) . All inference occurs in Vertex AI. The results are stored in BigQuery.

To learn more, try [understanding text with the `  ML.UNDERSTAND_TEXT  ` function](/bigquery/docs/understand-text) .

## Machine translation

You can use machine translation to translate text data into other languages. For example, translating customer feedback from an unfamiliar language into a familiar one.

To perform machine translation tasks, you can create a reference to the [Cloud Translation API](/translate) by creating a remote model and specifying `  CLOUD_AI_TRANSLATE_V3  ` for the `  REMOTE_SERVICE_TYPE  ` value. You can then use the [`  ML.TRANSLATE  ` function](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-translate) to interact with that service. `  ML.TRANSLATE  ` works with data in [standard tables](/bigquery/docs/tables-intro#standard-tables) . All inference occurs in Vertex AI. The results are stored in BigQuery.

To learn more, try [translating text with the `  ML.TRANSLATE  ` function](/bigquery/docs/translate-text) .

## Audio transcription

You can use audio transcription to transcribe audio files into written text. For example, transcribing a voicemail recording into a text message.

To perform audio transcription tasks, you can create a reference to the [Speech-to-Text API](/speech-to-text) by creating a remote model and specifying `  CLOUD_AI_SPEECH_TO_TEXT_V2  ` for the `  REMOTE_SERVICE_TYPE  ` value. You can optionally [specify a recognizer to use](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-service#speech_recognizer) to process the audio content. You can then use the [`  ML.TRANSCRIBE  ` function](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-transcribe) to transcribe audio files. `  ML.TRANSCRIBE  ` works with audio files in [object tables](/bigquery/docs/object-table-introduction) . All inference occurs in Vertex AI. The results are stored in BigQuery.

To learn more, try [transcribing audio files with the `  ML.TRANSCRIBE  ` function](/bigquery/docs/transcribe) .

## Document processing

You can use document processing to extract insights from unstructured documents. For example, extracting relevant information from invoice files so it can be input into accounting software.

To perform document processing tasks, you can create a reference to the [Document AI API](/document-ai) by creating a remote model, specifying `  CLOUD_AI_DOCUMENT_V1  ` for the `  REMOTE_SERVICE_TYPE  ` value, and [specifying a processor to use](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-service#document_processor) to process the document content. You can then use the [`  ML.PROCESS_DOCUMENT  ` function](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-process-document) to process documents. `  ML.PROCESS_DOCUMENT  ` works on documents in [object tables](/bigquery/docs/object-table-introduction) . All inference occurs in Vertex AI. The results are stored in BigQuery.

To learn more, try [processing documents with the `  ML.PROCESS_DOCUMENT  ` function](/bigquery/docs/process-document) .

## Computer vision

You can use computer vision to perform image analysis tasks. For example, you could analyze images to detect whether they contain faces, or to generate labels describing the objects in the image.

To perform computer vision tasks, you can create a reference to the [Cloud Vision API](/vision) by creating a remote model and specifying `  CLOUD_AI_VISION_V1  ` for the `  REMOTE_SERVICE_TYPE  ` value. You can then use the [`  ML.ANNOTATE_IMAGE  ` function](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-annotate-image) to annotate images by using that service. `  ML.ANNOTATE_IMAGE  ` works with data in [object tables](/bigquery/docs/object-table-introduction) . All inference occurs in Vertex AI. The results are stored in BigQuery.

To learn more, try [annotating object table images with the `  ML.ANNOTATE_IMAGE  ` function](/bigquery/docs/annotate-image) .

## What's next

  - For more information about performing inference over machine learning models, see [Model inference overview](/bigquery/docs/inference-overview) .
  - For more information about supported SQL statements and functions for generative AI models, see [End-to-end user journeys for generative AI models](/bigquery/docs/e2e-journey-genai) .
