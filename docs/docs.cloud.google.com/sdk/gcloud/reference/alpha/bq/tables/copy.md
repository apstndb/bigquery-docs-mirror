---
name: documents/docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/tables/copy
uri: https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/tables/copy
title: gcloud alpha bq tables copy
description: Offers tools and libraries that allow you to create and manage resources across Google Cloud.
data_source: docs.cloud.google.com
---

NAME

gcloud alpha bq tables copy - copy one BigQuery table to another

SYNOPSIS

`gcloud alpha bq tables copy` ( [`--destination`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/tables/copy#--destination) = `DESTINATION` : [`--destination-dataset`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/tables/copy#--destination-dataset) = `DESTINATION_DATASET` ) ( [`--source`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/tables/copy#--source) = `SOURCE` : [`--source-dataset`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/tables/copy#--source-dataset) = `SOURCE_DATASET` ) \[ [`--async`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/tables/copy#--async) \] \[ [`--job-id`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/tables/copy#--job-id) = `JOB_ID` \] \[ [`--overwrite`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/tables/copy#--overwrite) \] \[ [`GCLOUD_WIDE_FLAG`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/tables/copy#GCLOUD-WIDE-FLAGS)` …` \]

DESCRIPTION

`(ALPHA)` `gcloud alpha bq tables copy` Copies one BigQuery table to another.

EXAMPLES

The following copies table `my-table` to table `my-other-table` , in dataset `my-dataset` overwriting destination if it exists:

```
gcloud alpha bq tables copy --source my-table --destination my-other-table --source-dataset my-dataset --overwrite
```

REQUIRED FLAGS

Table resource - The destination to copy to. The arguments in this group can be used to specify the attributes of this resource. (NOTE) Some attributes are not given arguments in this group but can be set in other ways.

To set the `project` attribute:

- provide the argument `--destination` on the command line with a fully specified name;
- provide the argument `--project` on the command line;
- set the property `core/project` .

This must be specified.

`--destination` = `DESTINATION`  
ID of the table or fully qualified identifier for the table.

To set the `source` attribute:

- provide the argument `--destination` on the command line.

This flag argument must be specified if any of the other arguments in this group are specified.

`--destination-dataset` = `DESTINATION_DATASET`  
The id of the BigQuery dataset.

To set the `dataset` attribute:

- provide the argument `--destination` on the command line with a fully specified name;
- provide the argument `--destination-dataset` on the command line;
- provide the argument `--source-dataset` on the command line.

Table resource - The source to copy from. The arguments in this group can be used to specify the attributes of this resource. (NOTE) Some attributes are not given arguments in this group but can be set in other ways.

To set the `project` attribute:

- provide the argument `--source` on the command line with a fully specified name;
- provide the argument `--project` on the command line;
- set the property `core/project` .

This must be specified.

`--source` = `SOURCE`  
ID of the table or fully qualified identifier for the table.

To set the `source` attribute:

- provide the argument `--source` on the command line.

This flag argument must be specified if any of the other arguments in this group are specified.

`--source-dataset` = `SOURCE_DATASET`  
The id of the BigQuery dataset.

To set the `dataset` attribute:

- provide the argument `--source` on the command line with a fully specified name;
- provide the argument `--source-dataset` on the command line;
- provide the argument `--destination-dataset` on the command line.

OPTIONAL FLAGS

`--async`  
Return immediately, without waiting for the operation in progress to complete.

`--job-id` = `JOB_ID`  
A unique job ID to use for the request. If not specified a unique job id will be generated.

`--overwrite`  
Overwrite if the resource already exists.

GCLOUD WIDE FLAGS

These flags are available to all commands: [`--access-token-file`](https://docs.cloud.google.com/sdk/gcloud/reference#--access-token-file) , [`--account`](https://docs.cloud.google.com/sdk/gcloud/reference#--account) , [`--billing-project`](https://docs.cloud.google.com/sdk/gcloud/reference#--billing-project) , [`--configuration`](https://docs.cloud.google.com/sdk/gcloud/reference#--configuration) , [`--flags-file`](https://docs.cloud.google.com/sdk/gcloud/reference#--flags-file) , [`--flatten`](https://docs.cloud.google.com/sdk/gcloud/reference#--flatten) , [`--format`](https://docs.cloud.google.com/sdk/gcloud/reference#--format) , [`--help`](https://docs.cloud.google.com/sdk/gcloud/reference#--help) , [`--impersonate-service-account`](https://docs.cloud.google.com/sdk/gcloud/reference#--impersonate-service-account) , [`--log-http`](https://docs.cloud.google.com/sdk/gcloud/reference#--log-http) , [`--project`](https://docs.cloud.google.com/sdk/gcloud/reference#--project) , [`--quiet`](https://docs.cloud.google.com/sdk/gcloud/reference#--quiet) , [`--trace-token`](https://docs.cloud.google.com/sdk/gcloud/reference#--trace-token) , [`--user-output-enabled`](https://docs.cloud.google.com/sdk/gcloud/reference#--user-output-enabled) , [`--verbosity`](https://docs.cloud.google.com/sdk/gcloud/reference#--verbosity) .

Run `$ `[`gcloud help`](https://docs.cloud.google.com/sdk/gcloud/reference) for details.

NOTES

This command is currently in alpha and might change without notice. If this command fails with API permission errors despite specifying the correct project, you might be trying to access an API with an invitation-only early access allowlist.
