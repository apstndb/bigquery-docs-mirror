---
name: documents/docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/jobs/cancel
uri: https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/jobs/cancel
title: gcloud alpha bq jobs cancel
description: Offers tools and libraries that allow you to create and manage resources across Google Cloud.
data_source: docs.cloud.google.com
---

NAME

gcloud alpha bq jobs cancel - cancel a BigQuery job

SYNOPSIS

`gcloud alpha bq jobs cancel` [`JOB`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/jobs/cancel#JOB) \[ [`GCLOUD_WIDE_FLAG`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/jobs/cancel#GCLOUD-WIDE-FLAGS)` …` \]

DESCRIPTION

`(ALPHA)` Cancel a BigQuery job.

EXAMPLES

The following command cancels a job named `my-query-job` and returns the final state of the job:

```
gcloud alpha bq jobs cancel my-query-job
```

POSITIONAL ARGUMENTS

Job resource - The BigQuery job to cancel. This represents a Cloud resource. (NOTE) Some attributes are not given arguments in this group but can be set in other ways.

To set the `project` attribute:

- provide the argument `job` on the command line with a fully specified name;
- provide the argument `--project` on the command line;
- set the property `core/project` .

This must be specified.

`JOB`  
ID of the job or fully qualified identifier for the job.

To set the `job` attribute:

- provide the argument `job` on the command line.

GCLOUD WIDE FLAGS

These flags are available to all commands: [`--access-token-file`](https://docs.cloud.google.com/sdk/gcloud/reference#--access-token-file) , [`--account`](https://docs.cloud.google.com/sdk/gcloud/reference#--account) , [`--billing-project`](https://docs.cloud.google.com/sdk/gcloud/reference#--billing-project) , [`--configuration`](https://docs.cloud.google.com/sdk/gcloud/reference#--configuration) , [`--flags-file`](https://docs.cloud.google.com/sdk/gcloud/reference#--flags-file) , [`--flatten`](https://docs.cloud.google.com/sdk/gcloud/reference#--flatten) , [`--format`](https://docs.cloud.google.com/sdk/gcloud/reference#--format) , [`--help`](https://docs.cloud.google.com/sdk/gcloud/reference#--help) , [`--impersonate-service-account`](https://docs.cloud.google.com/sdk/gcloud/reference#--impersonate-service-account) , [`--log-http`](https://docs.cloud.google.com/sdk/gcloud/reference#--log-http) , [`--project`](https://docs.cloud.google.com/sdk/gcloud/reference#--project) , [`--quiet`](https://docs.cloud.google.com/sdk/gcloud/reference#--quiet) , [`--trace-token`](https://docs.cloud.google.com/sdk/gcloud/reference#--trace-token) , [`--user-output-enabled`](https://docs.cloud.google.com/sdk/gcloud/reference#--user-output-enabled) , [`--verbosity`](https://docs.cloud.google.com/sdk/gcloud/reference#--verbosity) .

Run `$ `[`gcloud help`](https://docs.cloud.google.com/sdk/gcloud/reference) for details.

API REFERENCE

This command uses the `bigquery/v2` API. The full documentation for this API can be found at: <https://cloud.google.com/bigquery/>

NOTES

This command is currently in alpha and might change without notice. If this command fails with API permission errors despite specifying the correct project, you might be trying to access an API with an invitation-only early access allowlist.
