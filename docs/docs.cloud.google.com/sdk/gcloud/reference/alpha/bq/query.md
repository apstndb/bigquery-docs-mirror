---
name: documents/docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/query
uri: https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/query
title: gcloud alpha bq query
description: Offers tools and libraries that allow you to create and manage resources across Google Cloud.
data_source: docs.cloud.google.com
---

NAME

gcloud alpha bq query - execute a BigQuery SQL query

SYNOPSIS

`gcloud alpha bq query` \[ [`SQL_QUERY`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/query#SQL_QUERY) \] \[ [`--async`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/query#--async) \] \[ [`--endpoint-mode`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/query#--endpoint-mode) = `ENDPOINT_MODE` \] \[ [`--job-creation-mode`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/query#--job-creation-mode) = `JOB_CREATION_MODE` \] \[ [`--job-id`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/query#--job-id) = `JOB_ID` \] \[ [`--location`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/query#--location) = `LOCATION` \] \[ [`--[no-]use-cache`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/query#--%5Bno-%5Duse-cache) \] \[ [`--[no-]use-legacy-sql`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/query#--%5Bno-%5Duse-legacy-sql) \] \[ [`GCLOUD_WIDE_FLAG`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/query#GCLOUD-WIDE-FLAGS)` …` \]

DESCRIPTION

`(ALPHA)` `gcloud alpha bq query` executes a SQL query on Google Cloud BigQuery.

The query can be passed as a positional argument or read from standard input (stdin).

EXAMPLES

To execute a simple query:

```
gcloud alpha bq query 'SELECT 1'
```

To execute a query passed through stdin:

```
echo 'SELECT 1' | gcloud alpha bq query
```

To run a query asynchronously with a custom job ID:

```
gcloud alpha bq query 'SELECT 1' --async --job-id=my-job-id
```

POSITIONAL ARGUMENTS

\[ `SQL_QUERY` \]  
SQL query to execute. If not specified, query will be read from stdin.

FLAGS

`--async`  
Return immediately, without waiting for the operation in progress to complete.

`--endpoint-mode` = `ENDPOINT_MODE`  
Specifies endpoint mode for a given command. Regional endpoints provide enhanced data residency and reliability by ensuring your request is handled entirely within the specified Google Cloud region. This differs from global endpoints, which may process parts of the request outside the target region. Overrides the default `regional/endpoint_mode` property value for this command invocation. `ENDPOINT_MODE` must be one of:

`global`  
(Default) Use global rather than regional endpoints.

`regional`  
Only use regional endpoints. An error will be raised if a regional endpoint is not available for a given command.

`regional-preferred`  
Use regional endpoints when available, otherwise use global endpoints. Recommended for most users.

`--job-creation-mode` = `JOB_CREATION_MODE`  
Specifies whether a job should be created. `JOB_CREATION_MODE` must be one of: `JOB_CREATION_REQUIRED` , `JOB_CREATION_OPTIONAL` .

`--job-id` = `JOB_ID`  
A unique job ID to use for the query job. Forces a job to be created and is incompatible with `--job-creation-mode=JOB_CREATION_OPTIONAL` .

`--location` = `LOCATION`  
The geographic location where the query should run.

`--[no-]use-cache`  
Whether to look for the result in the query cache. Use `--use-cache` to enable and `--no-use-cache` to disable.

`--[no-]use-legacy-sql`  
Whether to use BigQuery's legacy SQL dialect for this query. Use `--use-legacy-sql` to enable and `--no-use-legacy-sql` to disable.

GCLOUD WIDE FLAGS

These flags are available to all commands: [`--access-token-file`](https://docs.cloud.google.com/sdk/gcloud/reference#--access-token-file) , [`--account`](https://docs.cloud.google.com/sdk/gcloud/reference#--account) , [`--billing-project`](https://docs.cloud.google.com/sdk/gcloud/reference#--billing-project) , [`--configuration`](https://docs.cloud.google.com/sdk/gcloud/reference#--configuration) , [`--flags-file`](https://docs.cloud.google.com/sdk/gcloud/reference#--flags-file) , [`--flatten`](https://docs.cloud.google.com/sdk/gcloud/reference#--flatten) , [`--format`](https://docs.cloud.google.com/sdk/gcloud/reference#--format) , [`--help`](https://docs.cloud.google.com/sdk/gcloud/reference#--help) , [`--impersonate-service-account`](https://docs.cloud.google.com/sdk/gcloud/reference#--impersonate-service-account) , [`--log-http`](https://docs.cloud.google.com/sdk/gcloud/reference#--log-http) , [`--project`](https://docs.cloud.google.com/sdk/gcloud/reference#--project) , [`--quiet`](https://docs.cloud.google.com/sdk/gcloud/reference#--quiet) , [`--trace-token`](https://docs.cloud.google.com/sdk/gcloud/reference#--trace-token) , [`--user-output-enabled`](https://docs.cloud.google.com/sdk/gcloud/reference#--user-output-enabled) , [`--verbosity`](https://docs.cloud.google.com/sdk/gcloud/reference#--verbosity) .

Run `$ `[`gcloud help`](https://docs.cloud.google.com/sdk/gcloud/reference) for details.

REGIONAL ENDPOINTS

This command supports regional endpoints. To use regional endpoints for this command, use the `--endpoint-mode=regional-preferred` flag. To use regional endpoints by default, run `$ `[`gcloud config set`](https://docs.cloud.google.com/sdk/gcloud/reference/config/set)` regional/endpoint_mode regional-preferred` .

NOTES

This command is currently in alpha and might change without notice. If this command fails with API permission errors despite specifying the correct project, you might be trying to access an API with an invitation-only early access allowlist.
