---
name: documents/docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.tasks.assessment.v2alpha
uri: https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.tasks.assessment.v2alpha
title: Package google.cloud.bigquery.migration.tasks.assessment.v2alpha
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

## Index

  - `  AssessmentTaskDetails  ` (message)

## AssessmentTaskDetails

DEPRECATED\! Use the AssessmentTaskDetails defined in com.google.cloud.bigquery.migration.v2alpha.AssessmentTaskDetails instead. Assessment task details.

Fields

`input_path`

`string`

Required. The Cloud Storage path for assessment input files.

`output_dataset`

`string`

Required. The BigQuery dataset for output.

`querylogs_path`

`string`

Optional. An optional Cloud Storage path to write the query logs (which is then used as an input path on the translation task)

`data_source`

`string`

Required. The data source or data warehouse type (eg: TERADATA/REDSHIFT) from which the input data is extracted.
