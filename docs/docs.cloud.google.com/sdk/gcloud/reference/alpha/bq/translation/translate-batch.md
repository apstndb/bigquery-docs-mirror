---
name: documents/docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/translation/translate-batch
uri: https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/translation/translate-batch
title: gcloud alpha bq translation translate-batch
description: Offers tools and libraries that allow you to create and manage resources across Google Cloud.
data_source: docs.cloud.google.com
---

NAME

gcloud alpha bq translation translate-batch - translates a batch of SQL queries

SYNOPSIS

`gcloud alpha bq translation translate-batch` `  --location  ` = `  LOCATION  ` `  --source-dialect  ` = `  SOURCE_DIALECT  ` `  --target-dialect  ` = `  TARGET_DIALECT  ` `  --target-gcs-path  ` = `  TARGET_GCS_PATH  ` \[ `  --async  ` \] \[ `  --enable-ai-suggestion  ` \] \[ `  --endpoint-mode  ` = `  ENDPOINT_MODE  ` \] \[ `  --source-gcs-files  ` =\[ `  FILE_URI  ` , …\]\] \[ `  --source-gcs-uris  ` =\[ `  URI  ` , …\]\] \[ `  --source-local-dirs  ` =\[ `  LOCAL_DIR  ` = `  CLOUD_STORAGE_URI  ` , …\]\] \[ `  --source-local-files  ` =\[ `  LOCAL_FILE  ` = `  CLOUD_STORAGE_FILE_URI  ` , …\]\] \[ `  --target-types  ` =\[ `  TARGET_TYPE  ` , …\]\] \[ `  GCLOUD_WIDE_FLAG …  ` \]

EXAMPLES

To translate a batch of Teradata queries in Cloud Storage in location `us-central1` , run:

    gcloud alpha bq translation translate-batch --source-dialect=teradata --target-dialect=bigquery --location=us-central1 --source-gcs-uris=gs://my-bucket/queries/ --target-gcs-path=gs://my-bucket/output/

To upload queries from a local directory and translate them, run:

    gcloud alpha bq translation translate-batch --source-dialect=teradata --target-dialect=bigquery --location=us-central1 --source-local-dirs=./queries=gs://my-bucket/queries/ --target-gcs-path=gs://my-bucket/output/

REQUIRED FLAGS

  - `--location` = `  LOCATION  `  
    The location to execute the migration workflow.
  - `--source-dialect` = `  SOURCE_DIALECT  `  
    The dialect of the source SQL files.
  - `--target-dialect` = `  TARGET_DIALECT  `  
    The dialect of the target SQL files.
  - `--target-gcs-path` = `  TARGET_GCS_PATH  `  
    The Cloud Storage directory URI where the translated output will be written.

OPTIONAL FLAGS

  - `--async`  
    Return immediately, without waiting for the operation in progress to complete.
  - `--enable-ai-suggestion`  
    Enable AI suggestion to improve translation quality.
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
    Map of local directories to their corresponding Cloud Storage URIs (e.g., local\_dir=gs://bucket/path). The local directories will be uploaded to the specified Cloud Storage URIs before translation, and those Cloud Storage URIs will be automatically included in the translation job.
  - `--source-local-files` =\[ `  LOCAL_FILE  ` = `  CLOUD_STORAGE_FILE_URI  ` ,…\]  
    Map of local files to their corresponding Cloud Storage URIs (e.g., local\_file=gs://bucket/path/file.sql). The local files will be uploaded to the specified Cloud Storage URIs before translation, and those Cloud Storage URIs will be automatically included in the translation job.
  - `--target-types` =\[ `  TARGET_TYPE  ` ,…\]  
    List of output types to generate. Supported values include `sql` to translate SQL files, and `metadata` to translate metadata ZIP files into DDL statements and table mappings. Specify both to translate SQL files and metadata ZIP files in a single job, instead of running a separate `  gcloud alpha bq translation translate-metadata  ` command. Defaults to `sql` .

GCLOUD WIDE FLAGS

These flags are available to all commands: `  --access-token-file  ` , `  --account  ` , `  --billing-project  ` , `  --configuration  ` , `  --flags-file  ` , `  --flatten  ` , `  --format  ` , `  --help  ` , `  --impersonate-service-account  ` , `  --log-http  ` , `  --project  ` , `  --quiet  ` , `  --trace-token  ` , `  --user-output-enabled  ` , `  --verbosity  ` .

Run ` $ gcloud help  ` for details.

REGIONAL ENDPOINTS

This command supports regional endpoints. To use regional endpoints for this command, use the `--endpoint-mode=regional-preferred` flag. To use regional endpoints by default, run `$ gcloud config set regional/endpoint_mode regional-preferred` .

NOTES

This command is currently in alpha and might change without notice. If this command fails with API permission errors despite specifying the correct project, you might be trying to access an API with an invitation-only early access allowlist.
