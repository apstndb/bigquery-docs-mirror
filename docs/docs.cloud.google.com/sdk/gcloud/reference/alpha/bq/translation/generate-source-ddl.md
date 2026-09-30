---
name: documents/docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/translation/generate-source-ddl
uri: https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/translation/generate-source-ddl
title: gcloud alpha bq translation generate-source-ddl
description: Offers tools and libraries that allow you to create and manage resources across Google Cloud.
data_source: docs.cloud.google.com
---

NAME

gcloud alpha bq translation generate-source-ddl - generates source DDL schemas from a batch of SQL queries using AI

SYNOPSIS

`gcloud alpha bq translation generate-source-ddl` `  --location  ` = `  LOCATION  ` `  --source-dialect  ` = `  SOURCE_DIALECT  ` `  --target-dialect  ` = `  TARGET_DIALECT  ` `  --target-gcs-path  ` = `  TARGET_GCS_PATH  ` \[ `  --async  ` \] \[ `  --endpoint-mode  ` = `  ENDPOINT_MODE  ` \] \[ `  --source-gcs-files  ` =\[ `  FILE_URI  ` , …\]\] \[ `  --source-gcs-uris  ` =\[ `  URI  ` , …\]\] \[ `  --source-local-dirs  ` =\[ `  LOCAL_DIR  ` = `  CLOUD_STORAGE_URI  ` , …\]\] \[ `  --source-local-files  ` =\[ `  LOCAL_FILE  ` = `  CLOUD_STORAGE_FILE_URI  ` , …\]\] \[ `  GCLOUD_WIDE_FLAG …  ` \]

EXAMPLES

To generate source DDL schemas for Teradata queries in Cloud Storage in location `us-central1` , run:

    gcloud alpha bq translation generate-source-ddl --source-dialect=teradata --target-dialect=bigquery --location=us-central1 --source-gcs-uris=gs://my-bucket/queries/ --target-gcs-path=gs://my-bucket/ddl/

To upload queries from a local directory and generate source DDL schemas, run:

    gcloud alpha bq translation generate-source-ddl --source-dialect=teradata --target-dialect=bigquery --location=us-central1 --source-local-dirs=./queries=gs://my-bucket/queries/ --target-gcs-path=gs://my-bucket/ddl/

REQUIRED FLAGS

  - `--location` = `  LOCATION  `  
    The location to execute the migration workflow.
  - `--source-dialect` = `  SOURCE_DIALECT  `  
    The dialect of the source SQL files.
  - `--target-dialect` = `  TARGET_DIALECT  `  
    The dialect of the target SQL files.
  - `--target-gcs-path` = `  TARGET_GCS_PATH  `  
    The Cloud Storage base URI where generated outputs will be written.

OPTIONAL FLAGS

  - `--async`  
    Return immediately, without waiting for the operation in progress to complete.
  - `--endpoint-mode` = `  ENDPOINT_MODE  `  
    Specifies endpoint mode for a given command. Regional endpoints provide enhanced data residency and reliability by ensuring your request is handled entirely within the specified Google Cloud region. This differs from global endpoints, which may process parts of the request outside the target region. Overrides the default `regional/endpoint_mode` property value for this command invocation. `  ENDPOINT_MODE  ` must be one of:
      - `global`  
        (Default) Use global rather than regional endpoints.
      - `regional`  
        Only use regional endpoints. An error will be raised if a regional endpoint is not available for a given command.
      - `regional-preferred`  
        Use regional endpoints when available, otherwise use global endpoints. Recommended for most users.
  - `--source-gcs-files` =\[ `  FILE_URI  ` ,…\]  
    List of Cloud Storage URIs pointing to individual source files or additional files. Note: these files must not be located within the directory specified by --source-gcs-uris, or an error will occur.
  - `--source-gcs-uris` =\[ `  URI  ` ,…\]  
    List of Cloud Storage URI prefixes containing multiple source SQL files.
  - `--source-local-dirs` =\[ `  LOCAL_DIR  ` = `  CLOUD_STORAGE_URI  ` ,…\]  
    Map of local directories to their corresponding Cloud Storage URIs (e.g., local\_dir=gs://bucket/path). The local directories will be uploaded to the specified Cloud Storage URIs before generation, and those Cloud Storage URIs will be automatically included in the generation job.
  - `--source-local-files` =\[ `  LOCAL_FILE  ` = `  CLOUD_STORAGE_FILE_URI  ` ,…\]  
    Map of local files to their corresponding Cloud Storage URIs (e.g., local\_file=gs://bucket/path/file.sql). The local files will be uploaded to the specified Cloud Storage URIs before generation, and those Cloud Storage URIs will be automatically included in the generation job.

GCLOUD WIDE FLAGS

These flags are available to all commands: `  --access-token-file  ` , `  --account  ` , `  --billing-project  ` , `  --configuration  ` , `  --flags-file  ` , `  --flatten  ` , `  --format  ` , `  --help  ` , `  --impersonate-service-account  ` , `  --log-http  ` , `  --project  ` , `  --quiet  ` , `  --trace-token  ` , `  --user-output-enabled  ` , `  --verbosity  ` .

Run ` $ gcloud help  ` for details.

REGIONAL ENDPOINTS

This command supports regional endpoints. To use regional endpoints for this command, use the `--endpoint-mode=regional-preferred` flag. To use regional endpoints by default, run `$ gcloud config set regional/endpoint_mode regional-preferred` .

NOTES

This command is currently in alpha and might change without notice. If this command fails with API permission errors despite specifying the correct project, you might be trying to access an API with an invitation-only early access allowlist.
