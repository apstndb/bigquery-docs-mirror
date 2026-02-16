# Choose a text generation function

This document provides a comparison of the BigQuery ML [`  AI.GENERATE_TEXT  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-generate-text) and [`  AI.GENERATE  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-generate) text generation functions. You can use the information in this document to help you decide which function to use in cases where the functions have overlapping capabilities.

## Function similarities

The `  AI.GENERATE_TEXT  ` and `  AI.GENERATE  ` functions are similar in the following ways:

  - **Purpose** : Generate text by passing a prompt to a large language model (LLM).
  - **Billing** : Incur BigQuery ML charges for data processed. For more information, see [BigQuery ML pricing](https://cloud.google.com/bigquery/pricing#bigquery-ml-pricing) . Incur Vertex AI charges for calls to the LLM. If you are using a Gemini 2.0 or greater model, the call is billed at the batch API rate. For more information, see [Cost of building and deploying AI models in Vertex AI](/vertex-ai/generative-ai/pricing) .
  - **Scalability** : Process between 1 million and 10 million rows for each a 6-hour query job. Actual throughput depends on factors like the average token length in the input rows. For more information, see [Generative AI functions](/bigquery/quotas#generative_ai_functions) .
  - **Input data** : Support both text and unstructured data from BigQuery standard tables and object tables.

## Function differences

Use the following table to evaluate the differences between the `  AI.GENERATE_TEXT  ` and `  AI.GENERATE  ` functions:

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
<th><code dir="ltr" translate="no">       AI.GENERATE      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Function signature</td>
<td>A table-valued function that takes a table as input and returns a table as output.</td>
<td>A scalar function that takes a single value as input and returns a single value as output.</td>
</tr>
<tr class="even">
<td>Supported LLMs</td>
<td><ul>
<li>Gemini models</li>
<li>Partner models such as Anthropic Claude, Llama, and Mistral AI</li>
<li>open models</li>
</ul></td>
<td>Gemini models</td>
</tr>
<tr class="odd">
<td>Function output content</td>
<td><p>Function output content for Gemini models:</p>
<ul>
<li>Generated text</li>
<li>Responsible AI (RAI) results</li>
<li>Google Search grounding results, if enabled</li>
<li>LLM call status</li>
</ul>
<p>Function output content for other types of models:</p>
<ul>
<li>Generated text</li>
<li>LLM call status</li>
</ul></td>
<td><ul>
<li>Generated text</li>
<li>Full model response in JSON format</li>
<li>LLM call status</li>
</ul></td>
</tr>
<tr class="even">
<td>Function output format</td>
<td>Generated values are returned in a single JSON column or in separate table columns, depending on the <code dir="ltr" translate="no">       flatten_json_output      </code> argument value.</td>
<td>Generated values are returned as fields in a <code dir="ltr" translate="no">       STRUCT      </code> object.</td>
</tr>
<tr class="odd">
<td>User journey</td>
<td>You must create a <a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model#create_model_syntax">remote model</a> before using the function.</td>
<td>You can use the function directly, without the need to create a remote model.</td>
</tr>
<tr class="even">
<td>Permission setup</td>
<td>You must manually create a BigQuery connection, and grant the Vertex AI User role permission to the service account of the connection. You can skip this step if you are using the BigQuery <a href="/bigquery/docs/default-connections#example-remote-model">default connection</a> .</td>
<td>You can call this function using your <a href="/bigquery/docs/permissions-for-ai-functions">end-user credentials</a> .</td>
</tr>
<tr class="odd">
<td>Advantages</td>
<td>Allows for more flexible input and output formats.</td>
<td>Easier to integrate into SQL queries.</td>
</tr>
<tr class="even">
<td>Extended functions</td>
<td>You can use the <a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-generate-table"><code dir="ltr" translate="no">        AI.GENERATE_TABLE       </code> function</a> to generate output that is structured according to a SQL output schema that you specify.</td>
<td>You can use the <a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-generate-bool"><code dir="ltr" translate="no">        AI.GENERATE_BOOL       </code></a> , <a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-generate-int"><code dir="ltr" translate="no">        AI.GENERATE_INT       </code></a> , and <a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-generate-double"><code dir="ltr" translate="no">        AI.GENERATE_DOUBLE       </code></a> functions to generate different types of scalar values.</td>
</tr>
</tbody>
</table>
