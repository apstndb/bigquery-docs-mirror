---
name: documents/docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/migration/translate
uri: https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/migration/translate
title: gcloud alpha bq migration translate
description: Offers tools and libraries that allow you to create and manage resources across Google Cloud.
data_source: docs.cloud.google.com
---

NAME

gcloud alpha bq migration translate - translate a SQL query from a source dialect to BigQuery

SYNOPSIS

`gcloud alpha bq migration translate` [`--location`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/migration/translate#--location) = `LOCATION` [`--source-dialect`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/migration/translate#--source-dialect) = `SOURCE_DIALECT` [`--target-dialect`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/migration/translate#--target-dialect) = `TARGET_DIALECT` \[ [`--endpoint-mode`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/migration/translate#--endpoint-mode) = `ENDPOINT_MODE` \] \[ [`--explanation-output-file`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/migration/translate#--explanation-output-file) = `EXPLANATION_OUTPUT_FILE` \] \[ [`--input-file`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/migration/translate#--input-file) = `INPUT_FILE` \] \[ [`--metadata-gcs-uri`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/migration/translate#--metadata-gcs-uri) = `METADATA_GCS_URI` \] \[ [`--output-file`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/migration/translate#--output-file) = `OUTPUT_FILE` \] \[ [`--source-ddl-output-file`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/migration/translate#--source-ddl-output-file) = `SOURCE_DDL_OUTPUT_FILE` \] \[ [`--source-sql-suggestion-output-file`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/migration/translate#--source-sql-suggestion-output-file) = `SOURCE_SQL_SUGGESTION_OUTPUT_FILE` \] \[ [`--target-sql-suggestion-output-file`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/migration/translate#--target-sql-suggestion-output-file) = `TARGET_SQL_SUGGESTION_OUTPUT_FILE` \] \[ [`--translation-config-files`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/migration/translate#--translation-config-files) =\[ `CONFIG_FILE` , …\]\] \[ [`--translation-log-file`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/migration/translate#--translation-log-file) = `TRANSLATION_LOG_FILE` \] \[ [`GCLOUD_WIDE_FLAG`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/migration/translate#GCLOUD-WIDE-FLAGS)` …` \]

DESCRIPTION

`(ALPHA)` Translate a SQL query from a source dialect to BigQuery.

The command reads a SQL query from standard input (or an input file) and prints the translated query to standard output (or an output file).

EXAMPLES

To translate a Snowflake query from stdin, run:

```
echo 'SELECT * FROM test.my_table;' | gcloud alpha bq migration translate --source-dialect=SNOWFLAKE --target-dialect=BIGQUERY --location=us
```

To translate a Snowflake query from a file and save the output and logs to files, run:

```
gcloud alpha bq migration translate --source-dialect=SNOWFLAKE --target-dialect=BIGQUERY --location=us --project=my-project --input-file=input.sql --output-file=output.sql --translation-log-file=translation_logs.yaml
```

REQUIRED FLAGS

`--location` = `LOCATION`  
Google Cloud Storage location to use for the translation.

`--source-dialect` = `SOURCE_DIALECT`  
Source dialect of the query. See supported dialects in <https://docs.cloud.google.com/bigquery/docs/enable-sql-translations#supported_sql_dialects>

`--target-dialect` = `TARGET_DIALECT`  
Target dialect of the query. See supported dialects in <https://docs.cloud.google.com/bigquery/docs/enable-sql-translations#supported_sql_dialects>

OPTIONAL FLAGS

`--endpoint-mode` = `ENDPOINT_MODE`  
Specifies endpoint mode for a given command. Regional endpoints provide enhanced data residency and reliability by ensuring your request is handled entirely within the specified Google Cloud region. This differs from global endpoints, which may process parts of the request outside the target region. Overrides the default `regional/endpoint_mode` property value for this command invocation. `ENDPOINT_MODE` must be one of:

`global`  
(Default) Use global rather than regional endpoints.

`regional`  
Only use regional endpoints. An error will be raised if a regional endpoint is not available for a given command.

`regional-preferred`  
Use regional endpoints when available, otherwise use global endpoints. Recommended for most users.

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

`--source-sql-suggestion-output-file` = `SOURCE_SQL_SUGGESTION_OUTPUT_FILE`  
File to which to write the AI-customized source SQL generated by SOURCE_SQL rules in an .ai_config.yaml file before the query is processed by the translation engine. Writes to stdout if not provided when a source SQL suggestion is generated.

`--target-sql-suggestion-output-file` = `TARGET_SQL_SUGGESTION_OUTPUT_FILE`  
File to which to write the AI-customized target SQL generated by applying TARGET_SQL rules in an .ai_config.yaml file to the engine-translated SQL. Writes to stdout if not provided when a target SQL suggestion is generated.

`--translation-config-files` =\[ `CONFIG_FILE` ,…\]  
A comma-separated list of paths to YAML configuration files. File names must end with .config.yaml or .ai_config.yaml. See <https://docs.cloud.google.com/bigquery/docs/config-yaml-translation> for more details.

`--translation-log-file` = `TRANSLATION_LOG_FILE`  
File to which to write the translation logs.

GCLOUD WIDE FLAGS

These flags are available to all commands: [`--access-token-file`](https://docs.cloud.google.com/sdk/gcloud/reference#--access-token-file) , [`--account`](https://docs.cloud.google.com/sdk/gcloud/reference#--account) , [`--billing-project`](https://docs.cloud.google.com/sdk/gcloud/reference#--billing-project) , [`--configuration`](https://docs.cloud.google.com/sdk/gcloud/reference#--configuration) , [`--flags-file`](https://docs.cloud.google.com/sdk/gcloud/reference#--flags-file) , [`--flatten`](https://docs.cloud.google.com/sdk/gcloud/reference#--flatten) , [`--format`](https://docs.cloud.google.com/sdk/gcloud/reference#--format) , [`--help`](https://docs.cloud.google.com/sdk/gcloud/reference#--help) , [`--impersonate-service-account`](https://docs.cloud.google.com/sdk/gcloud/reference#--impersonate-service-account) , [`--log-http`](https://docs.cloud.google.com/sdk/gcloud/reference#--log-http) , [`--project`](https://docs.cloud.google.com/sdk/gcloud/reference#--project) , [`--quiet`](https://docs.cloud.google.com/sdk/gcloud/reference#--quiet) , [`--trace-token`](https://docs.cloud.google.com/sdk/gcloud/reference#--trace-token) , [`--user-output-enabled`](https://docs.cloud.google.com/sdk/gcloud/reference#--user-output-enabled) , [`--verbosity`](https://docs.cloud.google.com/sdk/gcloud/reference#--verbosity) .

Run `$ `[`gcloud help`](https://docs.cloud.google.com/sdk/gcloud/reference) for details.

REGIONAL ENDPOINTS

This command supports regional endpoints. To use regional endpoints for this command, use the `--endpoint-mode=regional-preferred` flag. To use regional endpoints by default, run `$ `[`gcloud config set`](https://docs.cloud.google.com/sdk/gcloud/reference/config/set)` regional/endpoint_mode regional-preferred` .

NOTES

This command is currently in alpha and might change without notice. If this command fails with API permission errors despite specifying the correct project, you might be trying to access an API with an invitation-only early access allowlist.
