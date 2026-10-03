---
name: documents/docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/translation/translate-metadata
uri: https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/translation/translate-metadata
title: gcloud alpha bq translation translate-metadata
description: Offers tools and libraries that allow you to create and manage resources across Google Cloud.
data_source: docs.cloud.google.com
---

NAME

gcloud alpha bq translation translate-metadata - translates metadata from zip files into DDL statements and table mappings

SYNOPSIS

`gcloud alpha bq translation translate-metadata` [`--location`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/translation/translate-metadata#--location) = `LOCATION` [`--source-dialect`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/translation/translate-metadata#--source-dialect) = `SOURCE_DIALECT` [`--target-dialect`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/translation/translate-metadata#--target-dialect) = `TARGET_DIALECT` [`--target-gcs-path`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/translation/translate-metadata#--target-gcs-path) = `TARGET_GCS_PATH` \[ [`--async`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/translation/translate-metadata#--async) \] \[ [`--endpoint-mode`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/translation/translate-metadata#--endpoint-mode) = `ENDPOINT_MODE` \] \[ [`--source-gcs-files`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/translation/translate-metadata#--source-gcs-files) =\[ `FILE_URI` , …\]\] \[ [`--source-gcs-uris`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/translation/translate-metadata#--source-gcs-uris) =\[ `URI` , …\]\] \[ [`--source-local-dirs`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/translation/translate-metadata#--source-local-dirs) =\[ `LOCAL_DIR` = `CLOUD_STORAGE_URI` , …\]\] \[ [`--source-local-files`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/translation/translate-metadata#--source-local-files) =\[ `LOCAL_FILE` = `CLOUD_STORAGE_FILE_URI` , …\]\] \[ [`GCLOUD_WIDE_FLAG`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/translation/translate-metadata#GCLOUD-WIDE-FLAGS)` …` \]

EXAMPLES

To translate Teradata metadata in Cloud Storage in location `us-central1` , run:

```
gcloud alpha bq translation translate-metadata --source-dialect=teradata --target-dialect=bigquery --location=us-central1 --source-gcs-uris=gs://my-bucket/metadata/ --target-gcs-path=gs://my-bucket/ddl_output/
```

To upload metadata from a local directory and translate it, run:

```
gcloud alpha bq translation translate-metadata --source-dialect=teradata --target-dialect=bigquery --location=us-central1 --source-local-dirs=./metadata=gs://my-bucket/metadata/ --target-gcs-path=gs://my-bucket/ddl_output/
```

REQUIRED FLAGS

`--location` = `LOCATION`  
The location to execute the translation.

`--source-dialect` = `SOURCE_DIALECT`  
The dialect of the source metadata.

`--target-dialect` = `TARGET_DIALECT`  
The dialect of the target tables.

`--target-gcs-path` = `TARGET_GCS_PATH`  
The Cloud Storage base URI where translated DDL outputs will be written.

OPTIONAL FLAGS

`--async`  
Return immediately, without waiting for the operation in progress to complete.

`--endpoint-mode` = `ENDPOINT_MODE`  
Specifies endpoint mode for a given command. Regional endpoints provide enhanced data residency and reliability by ensuring your request is handled entirely within the specified Google Cloud region. This differs from global endpoints, which may process parts of the request outside the target region. Overrides the default `regional/endpoint_mode` property value for this command invocation. `ENDPOINT_MODE` must be one of:

`global`  
(Default) Use global rather than regional endpoints.

`regional`  
Only use regional endpoints. An error will be raised if a regional endpoint is not available for a given command.

`regional-preferred`  
Use regional endpoints when available, otherwise use global endpoints. Recommended for most users.

`--source-gcs-files` =\[ `FILE_URI` ,…\]  
List of Cloud Storage URIs pointing to individual metadata zip files.

`--source-gcs-uris` =\[ `URI` ,…\]  
List of Cloud Storage URI prefixes containing metadata zip files.

`--source-local-dirs` =\[ `LOCAL_DIR` = `CLOUD_STORAGE_URI` ,…\]  
Map of local directories to their corresponding Cloud Storage URIs (e.g., local_dir=gs://bucket/path). The local directories will be uploaded to the specified Cloud Storage URIs before metadata translation, and those Cloud Storage URIs will be automatically included in the translation job.

`--source-local-files` =\[ `LOCAL_FILE` = `CLOUD_STORAGE_FILE_URI` ,…\]  
Map of local files to their corresponding Cloud Storage URIs (e.g., local_file=gs://bucket/path/file.zip). The local files will be uploaded to the specified Cloud Storage URIs before metadata translation, and those Cloud Storage URIs will be automatically included in the translation job.

GCLOUD WIDE FLAGS

These flags are available to all commands: [`--access-token-file`](https://docs.cloud.google.com/sdk/gcloud/reference#--access-token-file) , [`--account`](https://docs.cloud.google.com/sdk/gcloud/reference#--account) , [`--billing-project`](https://docs.cloud.google.com/sdk/gcloud/reference#--billing-project) , [`--configuration`](https://docs.cloud.google.com/sdk/gcloud/reference#--configuration) , [`--flags-file`](https://docs.cloud.google.com/sdk/gcloud/reference#--flags-file) , [`--flatten`](https://docs.cloud.google.com/sdk/gcloud/reference#--flatten) , [`--format`](https://docs.cloud.google.com/sdk/gcloud/reference#--format) , [`--help`](https://docs.cloud.google.com/sdk/gcloud/reference#--help) , [`--impersonate-service-account`](https://docs.cloud.google.com/sdk/gcloud/reference#--impersonate-service-account) , [`--log-http`](https://docs.cloud.google.com/sdk/gcloud/reference#--log-http) , [`--project`](https://docs.cloud.google.com/sdk/gcloud/reference#--project) , [`--quiet`](https://docs.cloud.google.com/sdk/gcloud/reference#--quiet) , [`--trace-token`](https://docs.cloud.google.com/sdk/gcloud/reference#--trace-token) , [`--user-output-enabled`](https://docs.cloud.google.com/sdk/gcloud/reference#--user-output-enabled) , [`--verbosity`](https://docs.cloud.google.com/sdk/gcloud/reference#--verbosity) .

Run `$ `[`gcloud help`](https://docs.cloud.google.com/sdk/gcloud/reference) for details.

REGIONAL ENDPOINTS

This command supports regional endpoints. To use regional endpoints for this command, use the `--endpoint-mode=regional-preferred` flag. To use regional endpoints by default, run `$ `[`gcloud config set`](https://docs.cloud.google.com/sdk/gcloud/reference/config/set)` regional/endpoint_mode regional-preferred` .

NOTES

This command is currently in alpha and might change without notice. If this command fails with API permission errors despite specifying the correct project, you might be trying to access an API with an invitation-only early access allowlist.
