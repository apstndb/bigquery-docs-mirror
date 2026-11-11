---
name: documents/docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/migration/validation/configure
uri: https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/migration/validation/configure
title: gcloud alpha bq migration validation configure
description: Offers tools and libraries that allow you to create and manage resources across Google Cloud.
data_source: docs.cloud.google.com
---

NAME

gcloud alpha bq migration validation configure - generate the configuration for validating migrated data

SYNOPSIS

`gcloud alpha bq migration validation configure` [`--output`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/migration/validation/configure#--output) = `DIRECTORY` ( [`--metadata`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/migration/validation/configure#--metadata) = `PATH` [`--tables-yaml`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/migration/validation/configure#--tables-yaml) =\[ `PATH` , …\]) \[ [`--endpoint-mode`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/migration/validation/configure#--endpoint-mode) = `ENDPOINT_MODE` \] \[ [`--force`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/migration/validation/configure#--force) \] \[ [`--schemas`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/migration/validation/configure#--schemas) =\[ `SCHEMA` , …\]\] \[ [`--tables`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/migration/validation/configure#--tables) =\[ `TABLE` , …\]\] \[ [`--target-dataset`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/migration/validation/configure#--target-dataset) = `TARGET_DATASET` \] \[ [`GCLOUD_WIDE_FLAG`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/migration/validation/configure#GCLOUD-WIDE-FLAGS)` …` \] \[-- [`CLIENT_ARGS`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/migration/validation/configure#CLIENT_ARGS) …\]

DESCRIPTION

`(ALPHA)` Generate the configuration files that [`gcloud alpha bq migration validation run`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/migration/validation/run) uses to validate data migrated to BigQuery against its source. The configuration covers the source tables described by a metadata archive produced by [`gcloud alpha bq migration metadata extract`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/migration/metadata/extract) ( `--metadata` ) and/or by the `tables.yaml` mapping files produced by BigQuery Migration Service SQL translation ( `--tables-yaml` ).

The output directory contains one YAML file per table under `databases/` , `index.yaml` listing the configured tables, `connections.yaml` with templates for the source and target connection profiles, and `settings.yaml` with the Cloud Storage location where source samples are staged and the results settings. Complete `connections.yaml` and `settings.yaml` before running the validation.

The configuration is generated on this machine by the BigQuery Migration Validation Client, which requires Java 11 or later on your `PATH` ; the `bqms` component of the gcloud CLI, which contains the client, is installed on first use if it is missing. To pass additional options to the Java virtual machine, set the `JAVA_OPTS` environment variable, for example `export JAVA_OPTS=-Xmx8G` (Linux and macOS) or `set JAVA_OPTS=-Xmx8G` (Windows Command Prompt).

Arguments after `--` are forwarded to the validation client unchanged. With `--quiet` , the client resolves ambiguities with defaults instead of prompting.

EXAMPLES

To generate configuration files under `./validation_config` for the tables in the Teradata metadata archive `dwh-migration-teradata-metadata.zip` , migrated to the BigQuery dataset `my_dataset` , run:

```
gcloud alpha bq migration validation configure --metadata=dwh-migration-teradata-metadata.zip --target-dataset=my_dataset --output=validation_config
```

To generate configuration files for the tables of the `sales` schema from the `tables.yaml` mapping files under `./translation_output` , overwriting any existing files under `./validation_config` , run:

```
gcloud alpha bq migration validation configure --tables-yaml=translation_output --schemas=sales --output=validation_config --force
```

POSITIONAL ARGUMENTS

\[-- `CLIENT_ARGS` …\]  
Arguments forwarded to the validation client.

The '--' argument must be specified between gcloud specific args on the left and CLIENT_ARGS on the right.

REQUIRED FLAGS

`--output` = `DIRECTORY`

Directory to write the configuration files to. Fails if the directory already contains files, unless `--force` is specified.

Source table definitions to generate the configuration from. Both can be combined.

At least one of these must be specified:

`--metadata` = `PATH`  
Path to a source metadata archive (a `.zip` file produced by [`gcloud alpha bq migration metadata extract`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/migration/metadata/extract) ), or to a directory containing such archives and `tables.yaml` translation mapping files.

`--tables-yaml` =\[ `PATH` ,…\]  
Paths to `tables.yaml` mapping files produced by BigQuery Migration Service SQL translation, or to directories containing them.

OPTIONAL FLAGS

`--endpoint-mode` = `ENDPOINT_MODE`  
Specifies endpoint mode for a given command. Regional endpoints provide enhanced data residency and reliability by ensuring your request is handled entirely within the specified Google Cloud region. This differs from global endpoints, which may process parts of the request outside the target region. Overrides the default `regional/endpoint_mode` property value for this command invocation. `ENDPOINT_MODE` must be one of:

`global`  
(Default) Use global rather than regional endpoints.

`regional`  
Only use regional endpoints. An error will be raised if a regional endpoint is not available for a given command.

`regional-preferred`  
Use regional endpoints when available, otherwise use global endpoints. Recommended for most users.

`--force`  
Overwrite existing configuration files in `--output` .

`--schemas` =\[ `SCHEMA` ,…\]  
Only generate configuration for tables in these source schemas.

`--tables` =\[ `TABLE` ,…\]  
Only generate configuration for these source tables.

`--target-dataset` = `TARGET_DATASET`  
BigQuery dataset that contains the migrated tables. Defaults to a dataset named like the schema of each source table.

GCLOUD WIDE FLAGS

These flags are available to all commands: [`--access-token-file`](https://docs.cloud.google.com/sdk/gcloud/reference#--access-token-file) , [`--account`](https://docs.cloud.google.com/sdk/gcloud/reference#--account) , [`--billing-project`](https://docs.cloud.google.com/sdk/gcloud/reference#--billing-project) , [`--configuration`](https://docs.cloud.google.com/sdk/gcloud/reference#--configuration) , [`--flags-file`](https://docs.cloud.google.com/sdk/gcloud/reference#--flags-file) , [`--flatten`](https://docs.cloud.google.com/sdk/gcloud/reference#--flatten) , [`--format`](https://docs.cloud.google.com/sdk/gcloud/reference#--format) , [`--help`](https://docs.cloud.google.com/sdk/gcloud/reference#--help) , [`--impersonate-service-account`](https://docs.cloud.google.com/sdk/gcloud/reference#--impersonate-service-account) , [`--log-http`](https://docs.cloud.google.com/sdk/gcloud/reference#--log-http) , [`--project`](https://docs.cloud.google.com/sdk/gcloud/reference#--project) , [`--quiet`](https://docs.cloud.google.com/sdk/gcloud/reference#--quiet) , [`--trace-token`](https://docs.cloud.google.com/sdk/gcloud/reference#--trace-token) , [`--user-output-enabled`](https://docs.cloud.google.com/sdk/gcloud/reference#--user-output-enabled) , [`--verbosity`](https://docs.cloud.google.com/sdk/gcloud/reference#--verbosity) .

Run `$ `[`gcloud help`](https://docs.cloud.google.com/sdk/gcloud/reference) for details.

REGIONAL ENDPOINTS

This command supports regional endpoints. To use regional endpoints for this command, use the `--endpoint-mode=regional-preferred` flag. To use regional endpoints by default, run `$ `[`gcloud config set`](https://docs.cloud.google.com/sdk/gcloud/reference/config/set)` regional/endpoint_mode regional-preferred` .

NOTES

This command is currently in alpha and might change without notice. If this command fails with API permission errors despite specifying the correct project, you might be trying to access an API with an invitation-only early access allowlist.
