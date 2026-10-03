---
name: documents/docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/tables/delete
uri: https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/tables/delete
title: gcloud alpha bq tables delete
description: Offers tools and libraries that allow you to create and manage resources across Google Cloud.
data_source: docs.cloud.google.com
---

NAME

gcloud alpha bq tables delete - delete a BigQuery table

SYNOPSIS

`gcloud alpha bq tables delete` ( [`TABLE`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/tables/delete#TABLE) : [`--dataset`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/tables/delete#--dataset) = `DATASET` ) \[ [`GCLOUD_WIDE_FLAG`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/tables/delete#GCLOUD-WIDE-FLAGS)` …` \]

DESCRIPTION

`(ALPHA)` Delete a BigQuery table.

EXAMPLES

The following command deletes a table with ID `my-table`

```
gcloud alpha bq tables delete my-table
```

POSITIONAL ARGUMENTS

Table resource - The BigQuery table you want to delete. The arguments in this group can be used to specify the attributes of this resource. (NOTE) Some attributes are not given arguments in this group but can be set in other ways.

To set the `project` attribute:

- provide the argument `table` on the command line with a fully specified name;
- provide the argument `--project` on the command line;
- set the property `core/project` .

This must be specified.

`TABLE`  
ID of the table or fully qualified identifier for the table.

To set the `table` attribute:

- provide the argument `table` on the command line.

This positional argument must be specified if any of the other arguments in this group are specified.

`--dataset` = `DATASET`  
The id of the BigQuery dataset.

To set the `dataset` attribute:

- provide the argument `table` on the command line with a fully specified name;
- provide the argument `--dataset` on the command line.

GCLOUD WIDE FLAGS

These flags are available to all commands: [`--access-token-file`](https://docs.cloud.google.com/sdk/gcloud/reference#--access-token-file) , [`--account`](https://docs.cloud.google.com/sdk/gcloud/reference#--account) , [`--billing-project`](https://docs.cloud.google.com/sdk/gcloud/reference#--billing-project) , [`--configuration`](https://docs.cloud.google.com/sdk/gcloud/reference#--configuration) , [`--flags-file`](https://docs.cloud.google.com/sdk/gcloud/reference#--flags-file) , [`--flatten`](https://docs.cloud.google.com/sdk/gcloud/reference#--flatten) , [`--format`](https://docs.cloud.google.com/sdk/gcloud/reference#--format) , [`--help`](https://docs.cloud.google.com/sdk/gcloud/reference#--help) , [`--impersonate-service-account`](https://docs.cloud.google.com/sdk/gcloud/reference#--impersonate-service-account) , [`--log-http`](https://docs.cloud.google.com/sdk/gcloud/reference#--log-http) , [`--project`](https://docs.cloud.google.com/sdk/gcloud/reference#--project) , [`--quiet`](https://docs.cloud.google.com/sdk/gcloud/reference#--quiet) , [`--trace-token`](https://docs.cloud.google.com/sdk/gcloud/reference#--trace-token) , [`--user-output-enabled`](https://docs.cloud.google.com/sdk/gcloud/reference#--user-output-enabled) , [`--verbosity`](https://docs.cloud.google.com/sdk/gcloud/reference#--verbosity) .

Run `$ `[`gcloud help`](https://docs.cloud.google.com/sdk/gcloud/reference) for details.

API REFERENCE

This command uses the `bigquery/v2` API. The full documentation for this API can be found at: <https://cloud.google.com/bigquery/>

NOTES

This command is currently in alpha and might change without notice. If this command fails with API permission errors despite specifying the correct project, you might be trying to access an API with an invitation-only early access allowlist.
