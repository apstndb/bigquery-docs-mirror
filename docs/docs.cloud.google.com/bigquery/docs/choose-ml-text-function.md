# Choose a natural language processing function

This document provides a comparison of the natural language processing functions available in BigQuery ML, which are [`  AI.GENERATE_TEXT  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-generate-text) , [`  ML.TRANSLATE  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-translate) , and [`  ML.UNDERSTAND_TEXT  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-understand-text) . You can use the information in this document to help you decide which function to use in cases where the functions have overlapping capabilities.

At a high level, the difference between these functions is as follows:

  - `  AI.GENERATE_TEXT  ` is a good choice for performing customized natural language processing (NLP) tasks at a lower cost. This function offers more language support, faster throughput, and model tuning capability, and also works with multimodal models.
  - `  ML.TRANSLATE  ` is a good choice for performing translation-specific NLP tasks where you need to support a high rate of queries per minute.
  - `  ML.UNDERSTAND_TEXT  ` is a good choice for performing NLP tasks that are supported by the Cloud Natural Language API.

## Function comparison

Use the following table to compare the `  AI.GENERATE_TEXT  ` , `  ML.TRANSLATE  ` , and `  ML.UNDERSTAND_TEXT  ` functions:

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th></th>
<th><code dir="ltr" translate="no">       AI.GENERATE_TEXT      </code></th>
<th><code dir="ltr" translate="no">       ML.TRANSLATE      </code></th>
<th><code dir="ltr" translate="no">       ML.UNDERSTAND_TEXT      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Purpose</td>
<td><p>Perform any NLP task by passing a prompt to a <a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model">Gemini or partner model</a> or to an <a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-open">open model</a> .</p>
<p>For example, to perform a question answering task, you could provide a prompt similar to <code dir="ltr" translate="no">        CONCAT("What are the key concepts in the following article?: ", article_text)       </code> .</p></td>
<td>Use the <a href="/translate">Cloud Translation API</a> to perform the following tasks:
<ul>
<li><a href="/translate/docs/advanced/translating-text-v3"><code dir="ltr" translate="no">          TRANSLATE_TEXT         </code></a></li>
<li><a href="/translate/docs/advanced/detecting-language-v3"><code dir="ltr" translate="no">          DETECT_LANGUAGE         </code></a></li>
</ul></td>
<td>Use the <a href="/natural-language">Cloud Natural Language API</a> to perform the following tasks:
<ul>
<li><a href="/natural-language/docs/analyzing-entities"><code dir="ltr" translate="no">          ANALYZE_ENTITIES         </code></a></li>
<li><a href="/natural-language/docs/analyzing-entity-sentiment"><code dir="ltr" translate="no">          ANALYZE_ENTITY_SENTIMENT         </code></a></li>
<li><a href="/natural-language/docs/analyzing-sentiment"><code dir="ltr" translate="no">          ANALYZE_SENTIMENT         </code></a></li>
<li><a href="/natural-language/docs/analyzing-syntax"><code dir="ltr" translate="no">          ANALYZE_SYNTAX         </code></a></li>
<li><a href="/natural-language/docs/classifying-text"><code dir="ltr" translate="no">          CLASSIFY_TEXT         </code></a></li>
</ul></td>
</tr>
<tr class="even">
<td>Billing</td>
<td><p>Incurs BigQuery ML charges for data processed. For more information, see <a href="https://cloud.google.com/bigquery/pricing#bigquery-ml-pricing">BigQuery ML pricing</a> .</p>
<p>Incurs Vertex AI charges for calls to the model. If you are using a Gemini 2.0 or greater model, the call is billed at the batch API rate. For more information, see <a href="/vertex-ai/generative-ai/pricing">Cost of building and deploying AI models in Vertex AI</a> .</p></td>
<td>Incurs BigQuery ML charges for data processed. For more information, see <a href="https://cloud.google.com/bigquery/pricing#bigquery-ml-pricing">BigQuery ML pricing</a> .<br />
<br />
Incurs charges for calls to the Cloud Translation API. For more information, see <a href="/translate/pricing">Cloud Translation API pricing</a> .</td>
<td><p>Incurs BigQuery ML charges for data processed. For more information, see <a href="https://cloud.google.com/bigquery/pricing#bigquery-ml-pricing">BigQuery ML pricing</a> .</p>
<p>Incurs charges for calls to the Cloud Natural Language API. For more information, see <a href="/translate/pricing">Cloud Natural Language API pricing</a> .</p></td>
</tr>
<tr class="odd">
<td>Requests per minute</td>
<td>Not applicable for Gemini models. Between 25 and 60 for partner models. For more information, see <a href="/bigquery/quotas#requests_per_minute_limits">Requests per minute limits</a> .</td>
<td>200. For more information, see <a href="/bigquery/quotas#cloud_ai_service_functions">Cloud AI service functions</a> .</td>
<td>600. For more information, see <a href="/bigquery/quotas#cloud_ai_service_functions">Cloud AI service functions</a> .</td>
</tr>
<tr class="even">
<td>Tokens per minute</td>
<td>Ranges from 8,192 to over 1 million, depending on the model used.</td>
<td>No token limit. However, <code dir="ltr" translate="no">       ML_TRANSLATE      </code> does have a <a href="/translate/quotas#content-limit">30,000 bytes limit</a> .</td>
<td><a href="/natural-language/quotas#content">100,000</a> .</td>
</tr>
<tr class="odd">
<td>Input data</td>
<td>Supports both text and unstructured data from BigQuery standard tables and object tables.</td>
<td>Supports text data from BigQuery standard tables.</td>
<td>Supports text data from BigQuery standard tables.</td>
</tr>
<tr class="even">
<td>Function output</td>
<td>Output can vary for calls to the model, even with the same prompt.</td>
<td>Produces the same output for a given task type for each successful call to the API. The output includes information about the input language.</td>
<td>Produces the same output for a given task type for each successful call to the API. The output includes information about the magnitude of the sentiment for sentiment analysis tasks.</td>
</tr>
<tr class="odd">
<td>Data context</td>
<td>You can provide data context as part of the prompt you submit.</td>
<td>Not supported.</td>
<td>Not supported.</td>
</tr>
<tr class="even">
<td>Supervised tuning</td>
<td><a href="/vertex-ai/generative-ai/docs/learn/models#languages-gemini">Supervised tuning</a> is supported for some models.</td>
<td>Not supported.</td>
<td>Not supported.</td>
</tr>
<tr class="odd">
<td>Supported languages</td>
<td>Support varies based on the LLM you choose.</td>
<td>Supports Cloud Translation API <a href="/translate/docs/languages">languages</a> .</td>
<td>Supports Cloud Natural Language API <a href="/natural-language/docs/languages">languages</a> .</td>
</tr>
<tr class="even">
<td>Supported regions</td>
<td>Supported in all Generative AI for Vertex AI <a href="/vertex-ai/generative-ai/docs/learn/locations#available-regions">regions</a> .</td>
<td>Supported in the <code dir="ltr" translate="no">       EU      </code> and <code dir="ltr" translate="no">       US      </code> multi-regions.</td>
<td>Supported in the <code dir="ltr" translate="no">       EU      </code> and <code dir="ltr" translate="no">       US      </code> multi-regions.</td>
</tr>
</tbody>
</table>
