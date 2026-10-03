---
name: documents/docs.cloud.google.com/sdk/gcloud/reference/beta/bq/migration-workflows/list
uri: https://docs.cloud.google.com/sdk/gcloud/reference/beta/bq/migration-workflows/list
title: gcloud beta bq migration-workflows list
description: Offers tools and libraries that allow you to create and manage resources across Google Cloud.
data_source: docs.cloud.google.com
---

NAME

gcloud beta bq migration-workflows list - list migration workflows

SYNOPSIS

`gcloud beta bq migration-workflows list` [`--location`](https://docs.cloud.google.com/sdk/gcloud/reference/beta/bq/migration-workflows/list#--location) = `LOCATION` \[ [`--endpoint-mode`](https://docs.cloud.google.com/sdk/gcloud/reference/beta/bq/migration-workflows/list#--endpoint-mode) = `ENDPOINT_MODE` \] \[ [`--filter`](https://docs.cloud.google.com/sdk/gcloud/reference/beta/bq/migration-workflows/list#--filter) = `EXPRESSION` \] \[ [`--limit`](https://docs.cloud.google.com/sdk/gcloud/reference/beta/bq/migration-workflows/list#--limit) = `LIMIT` \] \[ [`--page-size`](https://docs.cloud.google.com/sdk/gcloud/reference/beta/bq/migration-workflows/list#--page-size) = `PAGE_SIZE` \] \[ [`--sort-by`](https://docs.cloud.google.com/sdk/gcloud/reference/beta/bq/migration-workflows/list#--sort-by) =\[ `FIELD` , …\]\] \[ [`--uri`](https://docs.cloud.google.com/sdk/gcloud/reference/beta/bq/migration-workflows/list#--uri) \] \[ [`GCLOUD_WIDE_FLAG`](https://docs.cloud.google.com/sdk/gcloud/reference/beta/bq/migration-workflows/list#GCLOUD-WIDE-FLAGS)` …` \]

DESCRIPTION

`(BETA)` List migration workflows

EXAMPLES

To list all migration workflows in location `EU` , run:

```
gcloud beta bq migration-workflows list --location=eu
```

REQUIRED FLAGS

Location resource - The project and location of the migration workflows to list. Example: `projects/123/locations/us` This represents a Cloud resource. (NOTE) Some attributes are not given arguments in this group but can be set in other ways.

To set the `project` attribute:

- provide the argument `--location` on the command line with a fully specified name;
- provide the argument `--project` on the command line;
- set the property `core/project` .

This must be specified.

`--location` = `LOCATION`  
ID of the location or fully qualified identifier for the location.

To set the `location` attribute:

- provide the argument `--location` on the command line.

FLAGS

`--endpoint-mode` = `ENDPOINT_MODE`  
Specifies endpoint mode for a given command. Regional endpoints provide enhanced data residency and reliability by ensuring your request is handled entirely within the specified Google Cloud region. This differs from global endpoints, which may process parts of the request outside the target region. Overrides the default `regional/endpoint_mode` property value for this command invocation. `ENDPOINT_MODE` must be one of:

`global`  
(Default) Use global rather than regional endpoints.

`regional`  
Only use regional endpoints. An error will be raised if a regional endpoint is not available for a given command.

`regional-preferred`  
Use regional endpoints when available, otherwise use global endpoints. Recommended for most users.

LIST COMMAND FLAGS

`--filter` = `EXPRESSION`  
Apply a Boolean filter `EXPRESSION` to each resource item to be listed. If the expression evaluates `True` , then that item is listed. For more details and examples of filter expressions, run \$ [gcloud topic filters](https://docs.cloud.google.com/sdk/gcloud/reference/topic/filters) . This flag interacts with other flags that are applied in this order: `--flatten` , `--sort-by` , `--filter` , `--limit` .

`--limit` = `LIMIT`  
Maximum number of resources to list. The default is `unlimited` . This flag interacts with other flags that are applied in this order: `--flatten` , `--sort-by` , `--filter` , `--limit` .

`--page-size` = `PAGE_SIZE`  
Some services group resource list output into pages. This flag specifies the maximum number of resources per page. The default is determined by the service if it supports paging, otherwise it is `unlimited` (no paging). Paging may be applied before or after `--filter` and `--limit` depending on the service.

`--sort-by` =\[ `FIELD` ,…\]  
Comma-separated list of resource field key names to sort by. The default order is ascending. Prefix a field with \`\`\~´´ for descending order on that field. This flag interacts with other flags that are applied in this order: `--flatten` , `--sort-by` , `--filter` , `--limit` .

`--uri`  
Print a list of resource URIs instead of the default output, and change the command output to a list of URIs. If this flag is used with `--format` , the formatting is applied on this URI list. To display URIs alongside other keys instead, use the `uri()` transform.

GCLOUD WIDE FLAGS

These flags are available to all commands: [`--access-token-file`](https://docs.cloud.google.com/sdk/gcloud/reference#--access-token-file) , [`--account`](https://docs.cloud.google.com/sdk/gcloud/reference#--account) , [`--billing-project`](https://docs.cloud.google.com/sdk/gcloud/reference#--billing-project) , [`--configuration`](https://docs.cloud.google.com/sdk/gcloud/reference#--configuration) , [`--flags-file`](https://docs.cloud.google.com/sdk/gcloud/reference#--flags-file) , [`--flatten`](https://docs.cloud.google.com/sdk/gcloud/reference#--flatten) , [`--format`](https://docs.cloud.google.com/sdk/gcloud/reference#--format) , [`--help`](https://docs.cloud.google.com/sdk/gcloud/reference#--help) , [`--impersonate-service-account`](https://docs.cloud.google.com/sdk/gcloud/reference#--impersonate-service-account) , [`--log-http`](https://docs.cloud.google.com/sdk/gcloud/reference#--log-http) , [`--project`](https://docs.cloud.google.com/sdk/gcloud/reference#--project) , [`--quiet`](https://docs.cloud.google.com/sdk/gcloud/reference#--quiet) , [`--trace-token`](https://docs.cloud.google.com/sdk/gcloud/reference#--trace-token) , [`--user-output-enabled`](https://docs.cloud.google.com/sdk/gcloud/reference#--user-output-enabled) , [`--verbosity`](https://docs.cloud.google.com/sdk/gcloud/reference#--verbosity) .

Run `$ `[`gcloud help`](https://docs.cloud.google.com/sdk/gcloud/reference) for details.

API REFERENCE

This command uses the `bigquerymigration/v2` API. The full documentation for this API can be found at: <https://cloud.google.com/solutions/migration/dw2bq/dw-bq-migration-overview>

REGIONAL ENDPOINTS

This command supports regional endpoints. To use regional endpoints for this command, use the `--endpoint-mode=regional-preferred` flag. To use regional endpoints by default, run `$ `[`gcloud config set`](https://docs.cloud.google.com/sdk/gcloud/reference/config/set)` regional/endpoint_mode regional-preferred` .

NOTES

This command is currently in beta and might change without notice. These variants are also available:

```
gcloud bq migration-workflows list
```

```
gcloud alpha bq migration-workflows list
```
