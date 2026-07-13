---
name: documents/docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/tables/insert
uri: https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/tables/insert
title: gcloud alpha bq tables insert
description: Offers tools and libraries that allow you to create and manage resources across Google Cloud.
data_source: docs.cloud.google.com
---

NAME

gcloud alpha bq tables insert - insert records specified into an existing table

SYNOPSIS

`gcloud alpha bq tables insert` ( `  TABLE  ` : `  --dataset  ` = `  DATASET  ` ) `  --data  ` = `  PATH_TO_FILE  ` \[ `  GCLOUD_WIDE_FLAG …  ` \]

DESCRIPTION

`(ALPHA)` Insert records specified into an existing table.

EXAMPLES

The following command inserts rows from `data_file.json` into `my-table` in `my-dataset` :

    gcloud alpha bq tables insert --table /projects/myproject/datasets/my-dataset/tables/my-table --data data_file.json

POSITIONAL ARGUMENTS

Table resource - The BigQuery table you want to insert data into. The arguments in this group can be used to specify the attributes of this resource. (NOTE) Some attributes are not given arguments in this group but can be set in other ways.

To set the `project` attribute:

  - provide the argument `table` on the command line with a fully specified name;
  - provide the argument `--project` on the command line;
  - set the property `core/project` .

This must be specified.

  - `  TABLE  `  
    ID of the table or fully qualified identifier for the table.
    
    To set the `table` attribute:
    
      - provide the argument `table` on the command line.
    
    This positional argument must be specified if any of the other arguments in this group are specified.

  - `--dataset` = `  DATASET  `  
    The id of the BigQuery dataset.
    
    To set the `dataset` attribute:
    
      - provide the argument `table` on the command line with a fully specified name;
      - provide the argument `--dataset` on the command line.

REQUIRED FLAGS

  - `--data` = `  PATH_TO_FILE  `  
    The file containing the newline-delimited array of JSON objects representing rows to insert.
    
      - For example: \[ {"string\_col": "value1", "bool\_col": false}, {"string\_col": "value2", "bool\_col": true}, {"string\_col": "value3", "bool\_col": false}, {"string\_col": "value4", "bool\_col": true}, {"string\_col": "value5", "bool\_col": false}, \]
    
    Use a full or relative path to a local file containing the value of data.

GCLOUD WIDE FLAGS

These flags are available to all commands: `  --access-token-file  ` , `  --account  ` , `  --billing-project  ` , `  --configuration  ` , `  --flags-file  ` , `  --flatten  ` , `  --format  ` , `  --help  ` , `  --impersonate-service-account  ` , `  --log-http  ` , `  --project  ` , `  --quiet  ` , `  --trace-token  ` , `  --user-output-enabled  ` , `  --verbosity  ` .

Run ` $ gcloud help  ` for details.

API REFERENCE

This command uses the `bigquery/v2` API. The full documentation for this API can be found at: <https://cloud.google.com/bigquery/>

NOTES

This command is currently in alpha and might change without notice. If this command fails with API permission errors despite specifying the correct project, you might be trying to access an API with an invitation-only early access allowlist.
