---
name: documents/docs.cloud.google.com/sdk/gcloud/reference/bq/migration-workflows/delete
uri: https://docs.cloud.google.com/sdk/gcloud/reference/bq/migration-workflows/delete
title: gcloud bq migration-workflows delete
description: Offers tools and libraries that allow you to create and manage resources across Google Cloud.
data_source: docs.cloud.google.com
---

NAME

gcloud bq migration-workflows delete - delete migration workflows

SYNOPSIS

`gcloud bq migration-workflows delete` ( [`WORKFLOW`](https://docs.cloud.google.com/sdk/gcloud/reference/bq/migration-workflows/delete#WORKFLOW) : [`--location`](https://docs.cloud.google.com/sdk/gcloud/reference/bq/migration-workflows/delete#--location) = `LOCATION` ) \[ [`--endpoint-mode`](https://docs.cloud.google.com/sdk/gcloud/reference/bq/migration-workflows/delete#--endpoint-mode) = `ENDPOINT_MODE` \] \[ [`GCLOUD_WIDE_FLAG`](https://docs.cloud.google.com/sdk/gcloud/reference/bq/migration-workflows/delete#GCLOUD-WIDE-FLAGS)` …` \]

DESCRIPTION

Delete a migration workflow

EXAMPLES

To delete a migration workflow `projects/123/locations/eu/workflows/1234` , run:

```
gcloud bq migration-workflows delete projects/123/locations/eu/workflows/1234
```

POSITIONAL ARGUMENTS

Workflow resource - The unique identifier for the migration workflow. Example: `projects/123/locations/us/workflows/1234` The arguments in this group can be used to specify the attributes of this resource. (NOTE) Some attributes are not given arguments in this group but can be set in other ways.

To set the `project` attribute:

- provide the argument `workflow` on the command line with a fully specified name;
- provide the argument `--project` on the command line;
- set the property `core/project` .

This must be specified.

`WORKFLOW`  
ID of the workflow or fully qualified identifier for the workflow.

To set the `workflow` attribute:

- provide the argument `workflow` on the command line.

This positional argument must be specified if any of the other arguments in this group are specified.

`--location` = `LOCATION`  
The location id of the workflow resource.

To set the `location` attribute:

- provide the argument `workflow` on the command line with a fully specified name;
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

GCLOUD WIDE FLAGS

These flags are available to all commands: [`--access-token-file`](https://docs.cloud.google.com/sdk/gcloud/reference#--access-token-file) , [`--account`](https://docs.cloud.google.com/sdk/gcloud/reference#--account) , [`--billing-project`](https://docs.cloud.google.com/sdk/gcloud/reference#--billing-project) , [`--configuration`](https://docs.cloud.google.com/sdk/gcloud/reference#--configuration) , [`--flags-file`](https://docs.cloud.google.com/sdk/gcloud/reference#--flags-file) , [`--flatten`](https://docs.cloud.google.com/sdk/gcloud/reference#--flatten) , [`--format`](https://docs.cloud.google.com/sdk/gcloud/reference#--format) , [`--help`](https://docs.cloud.google.com/sdk/gcloud/reference#--help) , [`--impersonate-service-account`](https://docs.cloud.google.com/sdk/gcloud/reference#--impersonate-service-account) , [`--log-http`](https://docs.cloud.google.com/sdk/gcloud/reference#--log-http) , [`--project`](https://docs.cloud.google.com/sdk/gcloud/reference#--project) , [`--quiet`](https://docs.cloud.google.com/sdk/gcloud/reference#--quiet) , [`--trace-token`](https://docs.cloud.google.com/sdk/gcloud/reference#--trace-token) , [`--user-output-enabled`](https://docs.cloud.google.com/sdk/gcloud/reference#--user-output-enabled) , [`--verbosity`](https://docs.cloud.google.com/sdk/gcloud/reference#--verbosity) .

Run `$ `[`gcloud help`](https://docs.cloud.google.com/sdk/gcloud/reference) for details.

API REFERENCE

This command uses the `bigquerymigration/v2` API. The full documentation for this API can be found at: <https://cloud.google.com/solutions/migration/dw2bq/dw-bq-migration-overview>

REGIONAL ENDPOINTS

This command supports regional endpoints. To use regional endpoints for this command, use the `--endpoint-mode=regional-preferred` flag. To use regional endpoints by default, run `$ `[`gcloud config set`](https://docs.cloud.google.com/sdk/gcloud/reference/config/set)` regional/endpoint_mode regional-preferred` .

NOTES

These variants are also available:

```
gcloud alpha bq migration-workflows delete
```

```
gcloud beta bq migration-workflows delete
```
