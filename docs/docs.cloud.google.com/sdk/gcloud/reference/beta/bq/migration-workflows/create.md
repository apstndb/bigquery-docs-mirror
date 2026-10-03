---
name: documents/docs.cloud.google.com/sdk/gcloud/reference/beta/bq/migration-workflows/create
uri: https://docs.cloud.google.com/sdk/gcloud/reference/beta/bq/migration-workflows/create
title: gcloud beta bq migration-workflows create
description: Offers tools and libraries that allow you to create and manage resources across Google Cloud.
data_source: docs.cloud.google.com
---

NAME

gcloud beta bq migration-workflows create - create migration workflows

SYNOPSIS

`gcloud beta bq migration-workflows create` [`--config-file`](https://docs.cloud.google.com/sdk/gcloud/reference/beta/bq/migration-workflows/create#--config-file) = `CONFIG_FILE` [`--location`](https://docs.cloud.google.com/sdk/gcloud/reference/beta/bq/migration-workflows/create#--location) = `LOCATION` \[ [`--async`](https://docs.cloud.google.com/sdk/gcloud/reference/beta/bq/migration-workflows/create#--async) \] \[ [`GCLOUD_WIDE_FLAG`](https://docs.cloud.google.com/sdk/gcloud/reference/beta/bq/migration-workflows/create#GCLOUD-WIDE-FLAGS)` …` \]

DESCRIPTION

`(BETA)` Create a migration workflow

EXAMPLES

To create a migration workflow in EU synchronously based on a config file, run:

```
gcloud beta bq migration-workflows create --location=EU --config-file=config_file.yaml --no-async
```

REQUIRED FLAGS

`--config-file` = `CONFIG_FILE`  
Path to the migration workflows config file.

`--location` = `LOCATION`  
Location of the migration workflow.

OPTIONAL FLAGS

`--async`  
Return immediately, without waiting for the operation in progress to complete.

GCLOUD WIDE FLAGS

These flags are available to all commands: [`--access-token-file`](https://docs.cloud.google.com/sdk/gcloud/reference#--access-token-file) , [`--account`](https://docs.cloud.google.com/sdk/gcloud/reference#--account) , [`--billing-project`](https://docs.cloud.google.com/sdk/gcloud/reference#--billing-project) , [`--configuration`](https://docs.cloud.google.com/sdk/gcloud/reference#--configuration) , [`--flags-file`](https://docs.cloud.google.com/sdk/gcloud/reference#--flags-file) , [`--flatten`](https://docs.cloud.google.com/sdk/gcloud/reference#--flatten) , [`--format`](https://docs.cloud.google.com/sdk/gcloud/reference#--format) , [`--help`](https://docs.cloud.google.com/sdk/gcloud/reference#--help) , [`--impersonate-service-account`](https://docs.cloud.google.com/sdk/gcloud/reference#--impersonate-service-account) , [`--log-http`](https://docs.cloud.google.com/sdk/gcloud/reference#--log-http) , [`--project`](https://docs.cloud.google.com/sdk/gcloud/reference#--project) , [`--quiet`](https://docs.cloud.google.com/sdk/gcloud/reference#--quiet) , [`--trace-token`](https://docs.cloud.google.com/sdk/gcloud/reference#--trace-token) , [`--user-output-enabled`](https://docs.cloud.google.com/sdk/gcloud/reference#--user-output-enabled) , [`--verbosity`](https://docs.cloud.google.com/sdk/gcloud/reference#--verbosity) .

Run `$ `[`gcloud help`](https://docs.cloud.google.com/sdk/gcloud/reference) for details.

NOTES

This command is currently in beta and might change without notice. These variants are also available:

```
gcloud bq migration-workflows create
```

```
gcloud alpha bq migration-workflows create
```
