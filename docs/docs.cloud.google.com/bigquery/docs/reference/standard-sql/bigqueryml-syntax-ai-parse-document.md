---
name: documents/docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-parse-document
uri: https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-parse-document
title: The AI.PARSE_DOCUMENT function
description: Use AI.PARSE_DOCUMENT to parse documents and extract structured information, such as text chunks and page boundaries.
data_source: docs.cloud.google.com
---

# The AI.PARSE\_DOCUMENT function

> **Preview**
> 
> This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

> **Note:** To provide feedback or request support for this feature, send an email to <bqml-feedback@google.com> .

This document describes the `AI.PARSE_DOCUMENT` function, which parses documents such as PDFs and extracts structured information, including text chunks and page boundaries. It uses the Document AI [layout parser](https://docs.cloud.google.com/document-ai/docs/layout-parse-chunk) as the processing backend. This parser creates semantically coherent chunks that are augmented with contextual information.

To use this function, you must enable the Document AI API and [create a layout parser](https://docs.cloud.google.com/document-ai/docs/layout-parse-quickstart) .

## Syntax

```googlesql
AI.PARSE_DOCUMENT(
    { TABLE TABLE_NAME | (QUERY_STATEMENT) },
    endpoint => ENDPOINT
    [, chunk_size => CHUNK_SIZE ]
    [, connection_id => CONNECTION_ID ]
)
```

### Arguments

The `AI.PARSE_DOCUMENT` function takes the following arguments:

  - `  TABLE_NAME  ` : the name of the table that contains the documents to be parsed. The table must include a column named `ref` of type [`OBJECTREF`](https://docs.cloud.google.com/bigquery/docs/work-with-objectref) .

  - `  QUERY_STATEMENT  ` : a GoogleSQL query that produces the documents to be parsed. The query result must include a column named `ref` of type [`OBJECTREF`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/objectref_functions) .

  - `  ENDPOINT  ` : a `STRING` value that specifies the Document AI layout parser to use. You can provide the endpoint in one of the following formats:
    
      - Resource URL: `projects/{project}/locations/{location}/processors/{processor_id}`
      - Full Resource URL: `https://{region}-documentai.googleapis.com/v1/projects/{project}/locations/{location}/processors/{processor_id}:process`

  - `  CHUNK_SIZE  ` : an `INT64` value that specifies the chunk size for the layout parser to use. The default value is `1000` .

  - `  CONNECTION_ID  ` : a `STRING` value that specifies the [Cloud resource connection](https://docs.cloud.google.com/bigquery/docs/create-cloud-resource-connection) to use to communicate with the model, in the format ` [ PROJECT_ID ]. LOCATION . CONNECTION_ID  ` . For example, `myproject.us.myconnection` . You must grant the connection the Document AI Viewer role ( `roles/documentai.viewer` ) on the project in which you run the query.
    
    If you don't specify a connection, then the query uses your [end-user credentials](https://docs.cloud.google.com/bigquery/docs/permissions-for-ai-functions#run_generative_ai_queries_with_end-user_credentials) . If you use your end-user credentials, then you must have the Document AI Viewer role ( `roles/documentai.viewer` ) on the project in which you run the query.

## Output

The `AI.PARSE_DOCUMENT` function returns all columns from the input table in addition to the following columns:

  - `chunk_id` : an `INT64` value that contains the sequence ID of an extracted document chunk, starting from 1.
  - `start_page` : an `INT64` value that contains the page number where the chunk starts.
  - `end_page` : an `INT64` value that contains the page number where the chunk ends.
  - `content` : a `STRING` value that contains the extracted text content of the chunk.
  - `status` : a `STRING` value that contains the RPC status message. Returns an empty string on success, or an error message if the request fails.

## Limitations

An input document can have at most 130 pages.

## Examples

Before using `AI.PARSE_DOCUMENT` , you must first [create a layout parser](https://docs.cloud.google.com/document-ai/docs/layout-parse-quickstart) .

The following example parses a publicly available PDF of the first three pages of the Winnie-the-Pooh story. Replace the endpoint with your own layout parser:

    SELECT * EXCEPT(ref)
    FROM AI.PARSE_DOCUMENT(
      (
        SELECT
        OBJ.MAKE_REF("gs://cloud-samples-data/documentai/SampleDocuments/OCR_PROCESSOR/Winnie_the_Pooh_3_Pages.pdf") AS ref
      ),
      endpoint => "projects/123456789/locations/us/processors/123abc456def:process",
      chunk_size => 100
    );

The result is similar to the following:

    +----------+------------+----------+----------------------------------+--------+
    | chunk_id | start_page | end_page | content                          | status |
    +----------+------------+----------+----------------------------------+--------+
    | 1        | 1          | 3        | # CHAPTER I                      |        |
    |          |            |          |                                  |        |
    |          |            |          | IN WHICH We Are Introduced to    |        |
    |          |            |          | Winnie-the-Pooh and Some Bees,   |        |
    |          |            |          | and the Stories Begin...         |        |
    +----------+------------+----------+----------------------------------+--------+
    | 2        | 1          | 2        | When I first heard his name, I   |        |
    |          |            |          | said, just as you are going to   |        |
    |          |            |          | say, "But I thought he was a     |        |
    |          |            |          | boy?" "So did I," said           |        |
    |          |            |          | Christopher Robin. "Then you...  |        |
    +----------+------------+----------+----------------------------------+--------+
    | 3        | 2          | 2        | Sometimes Winnie-the-Pooh likes  |        |
    |          |            |          | a game of some sort when he      |        |
    |          |            |          | comes downstairs, and sometimes  |        |
    |          |            |          | he likes to sit quietly in front |        |
    |          |            |          | of the fire and listen to a...   |        |
    +----------+------------+----------+----------------------------------+--------+
    | ...      | ...        | ...      | ...                              | ...    |
    +----------+------------+----------+----------------------------------+--------+

The following example shows how to create an object table from Cloud Storage using the wildcard syntax to include multiple documents. Then you can pass the table directly as an argument to the `AI.PARSE_DOCUMENT` function:

    CREATE EXTERNAL TABLE mydataset.pdf_table
    WITH CONNECTION DEFAULT
    OPTIONS(
      object_metadata = 'SIMPLE',
      uris = ['gs://cloud-samples-data/bigquery/tutorials/cymbal-pets/document_chunks/*']);
    
    SELECT *
    FROM AI.PARSE_DOCUMENT(
      TABLE mydataset.pdf_table,
      endpoint => 'projects/123456789/locations/us/processors/123abc456def:process'
    );
