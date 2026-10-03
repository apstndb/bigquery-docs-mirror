---
name: documents/docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/translation/translate
uri: https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/translation/translate
title: gcloud alpha bq translation translate
description: Offers tools and libraries that allow you to create and manage resources across Google Cloud.
data_source: docs.cloud.google.com
---

NAME

gcloud alpha bq translation translate - translate a SQL query from a source dialect to BigQuery

SYNOPSIS

`gcloud alpha bq translation translate` [`--location`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/translation/translate#--location) = `LOCATION` [`--source-dialect`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/translation/translate#--source-dialect) = `SOURCE_DIALECT` [`--target-dialect`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/translation/translate#--target-dialect) = `TARGET_DIALECT` \[ [`--explanation-output-file`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/translation/translate#--explanation-output-file) = `EXPLANATION_OUTPUT_FILE` \] \[ [`--input-file`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/translation/translate#--input-file) = `INPUT_FILE` \] \[ [`--metadata-gcs-uri`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/translation/translate#--metadata-gcs-uri) = `METADATA_GCS_URI` \] \[ [`--output-file`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/translation/translate#--output-file) = `OUTPUT_FILE` \] \[ [`--source-ddl-output-file`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/translation/translate#--source-ddl-output-file) = `SOURCE_DDL_OUTPUT_FILE` \] \[ [`--translation-config-files`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/translation/translate#--translation-config-files) =\[ `CONFIG_FILE` , …\]\] \[ [`--translation-log-file`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/translation/translate#--translation-log-file) = `TRANSLATION_LOG_FILE` \] \[ [`GCLOUD_WIDE_FLAG`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/translation/translate#GCLOUD-WIDE-FLAGS)` …` \]

DESCRIPTION

`(ALPHA)` Translate a SQL query from a source dialect to BigQuery.

The command reads a SQL query from standard input (or an input file) and prints the translated query to standard output (or an output file).

EXAMPLES

To translate a Snowflake query from stdin, run:

```
echo 'SELECT * FROM test.my_table;' | gcloud alpha bq translation translate --source-dialect=SNOWFLAKE --target-dialect=BIGQUERY --location=us
```

To translate a Snowflake query from a file and save the output and logs to files, run:

```
gcloud alpha bq translation translate --source-dialect=SNOWFLAKE --target-dialect=BIGQUERY --location=us --project=my-project --input-file=input.sql --output-file=output.sql --translation-log-file=translation_logs.yaml
```

REQUIRED FLAGS

`--location` = `LOCATION`  
Google Cloud Storage location to use for the translation.

`--source-dialect` = `SOURCE_DIALECT`  
Source dialect of the query. See supported dialects in <https://docs.cloud.google.com/bigquery/docs/enable-sql-translations#supported_sql_dialects>

`--target-dialect` = `TARGET_DIALECT`  
Target dialect of the query. See supported dialects in <https://docs.cloud.google.com/bigquery/docs/enable-sql-translations#supported_sql_dialects>

OPTIONAL FLAGS

`--explanation-output-file` = `EXPLANATION_OUTPUT_FILE`  
File to which to write the translation explanation.

`--input-file` = `INPUT_FILE`  
File from which to read the SQL query to translate. Can be piped through stdin as well.

`--metadata-gcs-uri` = `METADATA_GCS_URI`  
Cloud Storage URI for the metadata zip file.

`--output-file` = `OUTPUT_FILE`  
File to which to write the translated SQL. Writes to stdout if not provided or if set to \`\`-´´.

`--source-ddl-output-file` = `SOURCE_DDL_OUTPUT_FILE`  
File to which to write the generated source DDL.

`--translation-config-files` =\[ `CONFIG_FILE` ,…\]  
A comma-separated list of paths to YAML configuration files. File names must end with .config.yaml. See <https://docs.cloud.google.com/bigquery/docs/config-yaml-translation> for more details.

`--translation-log-file` = `TRANSLATION_LOG_FILE`  
File to which to write the translation logs.

GCLOUD WIDE FLAGS

These flags are available to all commands: [`--access-token-file`](https://docs.cloud.google.com/sdk/gcloud/reference#--access-token-file) , [`--account`](https://docs.cloud.google.com/sdk/gcloud/reference#--account) , [`--billing-project`](https://docs.cloud.google.com/sdk/gcloud/reference#--billing-project) , [`--configuration`](https://docs.cloud.google.com/sdk/gcloud/reference#--configuration) , [`--flags-file`](https://docs.cloud.google.com/sdk/gcloud/reference#--flags-file) , [`--flatten`](https://docs.cloud.google.com/sdk/gcloud/reference#--flatten) , [`--format`](https://docs.cloud.google.com/sdk/gcloud/reference#--format) , [`--help`](https://docs.cloud.google.com/sdk/gcloud/reference#--help) , [`--impersonate-service-account`](https://docs.cloud.google.com/sdk/gcloud/reference#--impersonate-service-account) , [`--log-http`](https://docs.cloud.google.com/sdk/gcloud/reference#--log-http) , [`--project`](https://docs.cloud.google.com/sdk/gcloud/reference#--project) , [`--quiet`](https://docs.cloud.google.com/sdk/gcloud/reference#--quiet) , [`--trace-token`](https://docs.cloud.google.com/sdk/gcloud/reference#--trace-token) , [`--user-output-enabled`](https://docs.cloud.google.com/sdk/gcloud/reference#--user-output-enabled) , [`--verbosity`](https://docs.cloud.google.com/sdk/gcloud/reference#--verbosity) .

Run `$ `[`gcloud help`](https://docs.cloud.google.com/sdk/gcloud/reference) for details.

NOTES

This command is currently in alpha and might change without notice. If this command fails with API permission errors despite specifying the correct project, you might be trying to access an API with an invitation-only early access allowlist.
