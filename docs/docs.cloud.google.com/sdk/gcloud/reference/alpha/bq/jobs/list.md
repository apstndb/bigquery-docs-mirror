---
name: documents/docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/jobs/list
uri: https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/jobs/list
title: gcloud alpha bq jobs list
description: Offers tools and libraries that allow you to create and manage resources across Google Cloud.
data_source: docs.cloud.google.com
---

NAME

gcloud alpha bq jobs list - list all BigQuery jobs in a project

SYNOPSIS

`gcloud alpha bq jobs list` \[ [`--show-all-users`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/jobs/list#--show-all-users) \] \[ [`--show-config`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/jobs/list#--show-config) \] \[ [`--filter`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/jobs/list#--filter) = `EXPRESSION` \] \[ [`--limit`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/jobs/list#--limit) = `LIMIT` \] \[ [`--page-size`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/jobs/list#--page-size) = `PAGE_SIZE` \] \[ [`--sort-by`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/jobs/list#--sort-by) =\[ `FIELD` , …\]\] \[ [`GCLOUD_WIDE_FLAG`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/jobs/list#GCLOUD-WIDE-FLAGS)` …` \]

DESCRIPTION

`(ALPHA)` List all BigQuery jobs in a project.

EXAMPLES

The following command list all jobs in current project (for all users)

```
gcloud alpha bq jobs list --show-all-users
```

FLAGS

`--show-all-users`  
List jobs from all users.

`--show-config`  
Include job configuration in listing. Default is False.

LIST COMMAND FLAGS

`--filter` = `EXPRESSION`  
Apply a Boolean filter `EXPRESSION` to each resource item to be listed. If the expression evaluates `True` , then that item is listed. For more details and examples of filter expressions, run \$ [gcloud topic filters](https://docs.cloud.google.com/sdk/gcloud/reference/topic/filters) . This flag interacts with other flags that are applied in this order: `--flatten` , `--sort-by` , `--filter` , `--limit` .

`--limit` = `LIMIT`  
Maximum number of resources to list. The default is `unlimited` . This flag interacts with other flags that are applied in this order: `--flatten` , `--sort-by` , `--filter` , `--limit` .

`--page-size` = `PAGE_SIZE`  
Some services group resource list output into pages. This flag specifies the maximum number of resources per page. The default is determined by the service if it supports paging, otherwise it is `unlimited` (no paging). Paging may be applied before or after `--filter` and `--limit` depending on the service.

`--sort-by` =\[ `FIELD` ,…\]  
Comma-separated list of resource field key names to sort by. The default order is ascending. Prefix a field with \`\`\~´´ for descending order on that field. This flag interacts with other flags that are applied in this order: `--flatten` , `--sort-by` , `--filter` , `--limit` .

GCLOUD WIDE FLAGS

These flags are available to all commands: [`--access-token-file`](https://docs.cloud.google.com/sdk/gcloud/reference#--access-token-file) , [`--account`](https://docs.cloud.google.com/sdk/gcloud/reference#--account) , [`--billing-project`](https://docs.cloud.google.com/sdk/gcloud/reference#--billing-project) , [`--configuration`](https://docs.cloud.google.com/sdk/gcloud/reference#--configuration) , [`--flags-file`](https://docs.cloud.google.com/sdk/gcloud/reference#--flags-file) , [`--flatten`](https://docs.cloud.google.com/sdk/gcloud/reference#--flatten) , [`--format`](https://docs.cloud.google.com/sdk/gcloud/reference#--format) , [`--help`](https://docs.cloud.google.com/sdk/gcloud/reference#--help) , [`--impersonate-service-account`](https://docs.cloud.google.com/sdk/gcloud/reference#--impersonate-service-account) , [`--log-http`](https://docs.cloud.google.com/sdk/gcloud/reference#--log-http) , [`--project`](https://docs.cloud.google.com/sdk/gcloud/reference#--project) , [`--quiet`](https://docs.cloud.google.com/sdk/gcloud/reference#--quiet) , [`--trace-token`](https://docs.cloud.google.com/sdk/gcloud/reference#--trace-token) , [`--user-output-enabled`](https://docs.cloud.google.com/sdk/gcloud/reference#--user-output-enabled) , [`--verbosity`](https://docs.cloud.google.com/sdk/gcloud/reference#--verbosity) .

Run `$ `[`gcloud help`](https://docs.cloud.google.com/sdk/gcloud/reference) for details.

API REFERENCE

This command uses the `bigquery/v2` API. The full documentation for this API can be found at: <https://cloud.google.com/bigquery/>

NOTES

This command is currently in alpha and might change without notice. If this command fails with API permission errors despite specifying the correct project, you might be trying to access an API with an invitation-only early access allowlist.
