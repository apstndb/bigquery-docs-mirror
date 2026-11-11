---
name: documents/docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/migration/metadata/extract
uri: https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/migration/metadata/extract
title: gcloud alpha bq migration metadata extract
description: Offers tools and libraries that allow you to create and manage resources across Google Cloud.
data_source: docs.cloud.google.com
---

NAME

gcloud alpha bq migration metadata extract - extract metadata from a source data warehouse

SYNOPSIS

`gcloud alpha bq migration metadata extract` [`--connector`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/migration/metadata/extract#--connector) = `CONNECTOR` [`--output`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/migration/metadata/extract#--output) = `OUTPUT` \[ [`--endpoint-mode`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/migration/metadata/extract#--endpoint-mode) = `ENDPOINT_MODE` \] \[ [`--expected-owner`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/migration/metadata/extract#--expected-owner) = `EXPECTED_OWNER` \] \[ [`--run-mode`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/migration/metadata/extract#--run-mode) = `RUN_MODE` ; default="local"\] \[ [`--no-address`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/migration/metadata/extract#--address) [`--gce-instance`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/migration/metadata/extract#--gce-instance) = `GCE_INSTANCE` [`--gce-service-account`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/migration/metadata/extract#--gce-service-account) = `GCE_SERVICE_ACCOUNT` [`--gce-startup-script-url`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/migration/metadata/extract#--gce-startup-script-url) = `GCE_STARTUP_SCRIPT_URL` [`--network`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/migration/metadata/extract#--network) = `NETWORK` [`--secret`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/migration/metadata/extract#--secret) = `SECRET` [`--service-account-user`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/migration/metadata/extract#--service-account-user) = `SERVICE_ACCOUNT_USER` [`--subnet`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/migration/metadata/extract#--subnet) = `SUBNET` [`--zone`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/migration/metadata/extract#--zone) = `ZONE` \] \[ [`GCLOUD_WIDE_FLAG`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/migration/metadata/extract#GCLOUD-WIDE-FLAGS)` …` \] \[-- [`EXTRACTOR_ARGS`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/migration/metadata/extract#EXTRACTOR_ARGS) …\]

DESCRIPTION

`(ALPHA)` Extract metadata from a source data warehouse.

By default ( `--run-mode=local` ), the extractor runs on this machine and writes its output archive to `--output` , which can be either a local file or directory path or a Cloud Storage URI ( `gs://bucket/path` ). Writing to Cloud Storage in local mode uses Application Default Credentials (for example, from [`gcloud auth application-default login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/application-default/login) ). Local mode requires Java 11 or later on your `PATH` ; the `bqms` component of the gcloud CLI, which contains the extractor, is installed on first use if it is missing. To pass additional options to the Java virtual machine, set the `JAVA_OPTS` environment variable, for example `export JAVA_OPTS=-Xmx8G` (Linux and macOS) or `set JAVA_OPTS=-Xmx8G` (Windows Command Prompt) for large extractions, or `-Djavax.net.ssl.trustStore=…` for a custom trust store.

With `--run-mode=cloud` , the extractor runs on a Compute Engine instance in your project instead and writes its output archive to the Cloud Storage URI given by `--output` . The forwarded arguments are passed to the instance through a Secret Manager secret (see `--secret` ); because the instance cannot prompt for input, include connection credentials such as `--password` in them.

When `--output` is a Cloud Storage URI ( `gs://bucket/path` ), the command verifies before running the extractor that the bucket belongs to `--expected-owner` (or the active `core/project` property if `--expected-owner` is not specified) and does not allow public access. This requires `storage.buckets.list` permission (for example, `roles/storage.bucketViewer` ) on the owner project, object write permissions ( `roles/storage.objectUser` or `roles/storage.objectCreator` ) on the bucket, and `storage.buckets.getIamPolicy` permission ( `roles/storage.admin` ) on the bucket if Public Access Prevention is not enforced on the bucket.

Arguments after `--` are forwarded to the extractor unchanged. For the available connectors and their arguments, see <https://cloud.google.com/bigquery/docs/generate-metadata> .

EXAMPLES

To extract Snowflake metadata to `gs://my-bucket/snowflake/` using the extractor on this machine (which prompts for the password), run:

```
gcloud alpha bq migration metadata extract --connector=snowflake --output=gs://my-bucket/snowflake/ -- --host=my-account.snowflakecomputing.com --user=my-user --database=MY_DB --warehouse=MY_WH
```

To run the same extraction on a Compute Engine instance in zone `us-central1-a` , run:

```
gcloud alpha bq migration metadata extract --connector=snowflake --output=gs://my-bucket/snowflake/ --run-mode=cloud --zone=us-central1-a -- --host=my-account.snowflakecomputing.com --user=my-user --password=my-password --database=MY_DB --warehouse=MY_WH
```

POSITIONAL ARGUMENTS

\[-- `EXTRACTOR_ARGS` …\]  
Arguments forwarded to the extractor.

The '--' argument must be specified between gcloud specific args on the left and EXTRACTOR_ARGS on the right.

REQUIRED FLAGS

`--connector` = `CONNECTOR`  
Metadata connector to use for extraction (for example, `snowflake` , `teradata` , or `redshift` ). Must be a metadata connector, not a query logs connector (do not use a `-logs` connector).

`--output` = `OUTPUT`  
Target path for the extracted archive: a Cloud Storage URI ( `gs://bucket/path` ) or, with `--run-mode=local` , a local file or directory path.

OPTIONAL FLAGS

`--endpoint-mode` = `ENDPOINT_MODE`

Specifies endpoint mode for a given command. Regional endpoints provide enhanced data residency and reliability by ensuring your request is handled entirely within the specified Google Cloud region. This differs from global endpoints, which may process parts of the request outside the target region. Overrides the default `regional/endpoint_mode` property value for this command invocation. `ENDPOINT_MODE` must be one of:

`global`  
(Default) Use global rather than regional endpoints.

`regional`  
Only use regional endpoints. An error will be raised if a regional endpoint is not available for a given command.

`regional-preferred`  
Use regional endpoints when available, otherwise use global endpoints. Recommended for most users.

`--expected-owner` = `EXPECTED_OWNER`

Expected owner project ID of the `--output` Cloud Storage bucket. Defaults to the active `core/project` property.

`--run-mode` = `RUN_MODE` ; default="local"

Run mode for the extractor. `RUN_MODE` must be one of: `local` , `cloud` .

Cloud run mode options (--run-mode=cloud).

`--no-address`

Do not assign external IP to Compute Engine instance.

`--gce-instance` = `GCE_INSTANCE`

Name of the Compute Engine instance.

`--gce-service-account` = `GCE_SERVICE_ACCOUNT`

Service account for Compute Engine instance.

`--gce-startup-script-url` = `GCE_STARTUP_SCRIPT_URL`

URL to startup script.

`--network` = `NETWORK`

Network for Compute Engine instance.

Secret resource - The secret used to pass the extractor arguments to the Compute Engine instance. This represents a Cloud resource. (NOTE) Some attributes are not given arguments in this group but can be set in other ways.

To set the `project` attribute:

- provide the argument `--secret` on the command line with a fully specified name;
- provide the argument `--project` on the command line;
- set the property `core/project` .

`--secret` = `SECRET`

ID of the secret or fully qualified identifier for the secret.

To set the `secret` attribute:

- provide the argument `--secret` on the command line.

`--service-account-user` = `SERVICE_ACCOUNT_USER`

User to grant serviceAccountUser role.

`--subnet` = `SUBNET`

Subnet for Compute Engine instance.

`--zone` = `ZONE`

Zone to launch Compute Engine instance.

GCLOUD WIDE FLAGS

These flags are available to all commands: [`--access-token-file`](https://docs.cloud.google.com/sdk/gcloud/reference#--access-token-file) , [`--account`](https://docs.cloud.google.com/sdk/gcloud/reference#--account) , [`--billing-project`](https://docs.cloud.google.com/sdk/gcloud/reference#--billing-project) , [`--configuration`](https://docs.cloud.google.com/sdk/gcloud/reference#--configuration) , [`--flags-file`](https://docs.cloud.google.com/sdk/gcloud/reference#--flags-file) , [`--flatten`](https://docs.cloud.google.com/sdk/gcloud/reference#--flatten) , [`--format`](https://docs.cloud.google.com/sdk/gcloud/reference#--format) , [`--help`](https://docs.cloud.google.com/sdk/gcloud/reference#--help) , [`--impersonate-service-account`](https://docs.cloud.google.com/sdk/gcloud/reference#--impersonate-service-account) , [`--log-http`](https://docs.cloud.google.com/sdk/gcloud/reference#--log-http) , [`--project`](https://docs.cloud.google.com/sdk/gcloud/reference#--project) , [`--quiet`](https://docs.cloud.google.com/sdk/gcloud/reference#--quiet) , [`--trace-token`](https://docs.cloud.google.com/sdk/gcloud/reference#--trace-token) , [`--user-output-enabled`](https://docs.cloud.google.com/sdk/gcloud/reference#--user-output-enabled) , [`--verbosity`](https://docs.cloud.google.com/sdk/gcloud/reference#--verbosity) .

Run `$ `[`gcloud help`](https://docs.cloud.google.com/sdk/gcloud/reference) for details.

REGIONAL ENDPOINTS

This command supports regional endpoints. To use regional endpoints for this command, use the `--endpoint-mode=regional-preferred` flag. To use regional endpoints by default, run `$ `[`gcloud config set`](https://docs.cloud.google.com/sdk/gcloud/reference/config/set)` regional/endpoint_mode regional-preferred` .

NOTES

This command is currently in alpha and might change without notice. If this command fails with API permission errors despite specifying the correct project, you might be trying to access an API with an invitation-only early access allowlist.
