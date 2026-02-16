# Choose a document processing function

This document provides a comparison of the document processing functions available in BigQuery ML, which are [`  AI.GENERATE_TEXT  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-generate-text) and [`  ML.PROCESS_DOCUMENT  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-process-document) . You can use the information in this document to help you decide which function to use in cases where the functions have overlapping capabilities.

At a high level, the difference between these functions is as follows:

  - `  AI.GENERATE_TEXT  ` is a good choice for performing natural language processing (NLP) tasks where some of the content resides in documents. This function offers the following benefits:
    
      - Lower costs
      - More language support
      - Faster throughput
      - Model tuning capability
      - Availability of multimodal models
    
    For examples of document processing tasks that work best with this approach, see [Explore document processing capabilities with the Gemini API](https://ai.google.dev/gemini-api/docs/document-processing) .

  - `  ML.PROCESS_DOCUMENT  ` is a good choice for performing document processing tasks that require document parsing and a predefined, structured response.

## Function comparison

Use the following table to compare the `  AI.GENERATE_TEXT  ` and `  ML.PROCESS_DOCUMENT  ` functions:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th></th>
<th><code dir="ltr" translate="no">       AI.GENERATE_TEXT      </code></th>
<th><code dir="ltr" translate="no">       ML.PROCESS_DOCUMENT      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Purpose</td>
<td><p>Perform any document-related NLP task by passing a prompt to a <a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model">Gemini or partner model</a> or to an <a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-open">open model</a> .</p>
<p>For example, given a financial document for a company, you can retrieve document information by providing a prompt such as <code dir="ltr" translate="no">        What is       the quarterly revenue for each division?       </code> .</p></td>
<td>Use the <a href="/document-ai">Document AI API</a> to perform specialized document processing for different document types, such as invoices, tax forms, and financial statements. You can also perform document chunking.</td>
</tr>
<tr class="even">
<td>Billing</td>
<td><p>Incurs BigQuery ML charges for data processed. For more information, see <a href="https://cloud.google.com/bigquery/pricing#bigquery-ml-pricing">BigQuery ML pricing</a> .<br />
<br />
Incurs Vertex AI charges for calls to the model. If you are using a Gemini 2.0 or greater model, the call is billed at the batch API rate. For more information, see <a href="/vertex-ai/generative-ai/pricing">Cost of building and deploying AI models in Vertex AI</a> .</p></td>
<td>Incurs BigQuery ML charges for data processed. For more information, see <a href="https://cloud.google.com/bigquery/pricing#bigquery-ml-pricing">BigQuery ML pricing</a> .
<p>Incurs charges for calls to the Document AI API. For more information, see <a href="/document-ai/pricing">Document AI API pricing</a> .</p></td>
</tr>
<tr class="odd">
<td>Requests per minute (RPM)</td>
<td>Not applicable for Gemini models. Between 25 and 60 for partner models. For more information, see <a href="/bigquery/quotas#requests_per_minute_limits">Requests per minute limits</a> .</td>
<td>120 RPM per processor type, with an overall limit of 600 RPM per project. For more information, see <a href="/document-ai/quotas#quotas_list">Quotas list</a> .</td>
</tr>
<tr class="even">
<td>Tokens per minute</td>
<td>Ranges from 8,192 to over 1 million, depending on the model used.</td>
<td>No token limit. However, this function does have different page limits depending on the processor you use. For more information, see <a href="/document-ai/limits">Limits</a> .</td>
</tr>
<tr class="odd">
<td>Supervised tuning</td>
<td><a href="/vertex-ai/generative-ai/docs/learn/models#languages-gemini">Supervised tuning</a> is supported for some models.</td>
<td>Not supported.</td>
</tr>
<tr class="even">
<td>Supported languages</td>
<td>Support varies based on the LLM you choose.</td>
<td>Language support depends on the document processor type; most only support English. For more information, see <a href="/document-ai/docs/processors-list">Processor list</a> .</td>
</tr>
<tr class="odd">
<td>Supported regions</td>
<td>Supported in all Generative AI for Vertex AI <a href="/vertex-ai/generative-ai/docs/learn/locations#available-regions">regions</a> .</td>
<td>Supported in the <code dir="ltr" translate="no">       EU      </code> and <code dir="ltr" translate="no">       US      </code> multi-regions for all processors. Some processors are also available in certain single regions. For more information, see <a href="/document-ai/docs/regions">Regional and multi-regional support</a> .</td>
</tr>
</tbody>
</table>
