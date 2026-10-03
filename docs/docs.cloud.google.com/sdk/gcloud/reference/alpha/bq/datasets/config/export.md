---
name: documents/docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/datasets/config/export
uri: https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/datasets/config/export
title: gcloud alpha bq datasets config export
description: Offers tools and libraries that allow you to create and manage resources across Google Cloud.
data_source: docs.cloud.google.com
---

NAME

gcloud alpha bq datasets config export - export the configuration for a Google BigQuery dataset

SYNOPSIS

`gcloud alpha bq datasets config export` (\[ [`DATASET`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/datasets/config/export#DATASET) \]\] [`--all`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/datasets/config/export#--all) ) \[ [`--path`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/datasets/config/export#--path) = `PATH` ; default="-"\] \[ [`--resource-format`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/datasets/config/export#--resource-format) = `RESOURCE_FORMAT` \] \[ [`GCLOUD_WIDE_FLAG`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/datasets/config/export#GCLOUD-WIDE-FLAGS)` …` \]

DESCRIPTION

`(ALPHA)` `gcloud alpha bq datasets config export` exports the configuration for a Google BigQuery dataset.

Dataset configurations can be exported in Kubernetes Resource Model (krm) or Terraform HCL formats. The default format is `krm` .

Specifying `--all` allows you to export the configurations for all datasets within the project.

Specifying `--path` allows you to export the configuration(s) to a local directory.

EXAMPLES

To export the configuration for a dataset, run:

```
gcloud alpha bq datasets config export my-dataset
```

To export the configuration for a dataset to a file, run:

```
gcloud alpha bq datasets config export my-dataset --path=/path/to/dir/
```

To export the configuration for a dataset in Terraform HCL format, run:

```
gcloud alpha bq datasets config export my-dataset --resource-format=terraform
```

To export the configurations for all datasets within a project, run:

```
gcloud alpha bq datasets config export --all
```

POSITIONAL ARGUMENTS

Exactly one of these must be specified:

`DATASET`  
ID of the dataset or fully qualified identifier for the dataset.

To set the `dataset` attribute:

- provide the argument `dataset` on the command line.

`--all`  
Retrieve all resources within the project. If `--path` is specified and is a valid directory, resources will be output as individual files based on resource name and scope. If `--path` is not specified, resources will be streamed to stdout.

FLAGS

`--path` = `PATH` ; default="-"  
Path of the directory or file to output configuration(s). To output configurations to stdout, specify "--path=-".

`--resource-format` = `RESOURCE_FORMAT`  
Format of the configuration to export. Available configuration formats are Kubernetes Resource Model YAML (krm) or Terraform HCL (terraform). Command defaults to "krm". `RESOURCE_FORMAT` must be one of: `krm` , `terraform` .

GCLOUD WIDE FLAGS

These flags are available to all commands: [`--access-token-file`](https://docs.cloud.google.com/sdk/gcloud/reference#--access-token-file) , [`--account`](https://docs.cloud.google.com/sdk/gcloud/reference#--account) , [`--billing-project`](https://docs.cloud.google.com/sdk/gcloud/reference#--billing-project) , [`--configuration`](https://docs.cloud.google.com/sdk/gcloud/reference#--configuration) , [`--flags-file`](https://docs.cloud.google.com/sdk/gcloud/reference#--flags-file) , [`--flatten`](https://docs.cloud.google.com/sdk/gcloud/reference#--flatten) , [`--format`](https://docs.cloud.google.com/sdk/gcloud/reference#--format) , [`--help`](https://docs.cloud.google.com/sdk/gcloud/reference#--help) , [`--impersonate-service-account`](https://docs.cloud.google.com/sdk/gcloud/reference#--impersonate-service-account) , [`--log-http`](https://docs.cloud.google.com/sdk/gcloud/reference#--log-http) , [`--project`](https://docs.cloud.google.com/sdk/gcloud/reference#--project) , [`--quiet`](https://docs.cloud.google.com/sdk/gcloud/reference#--quiet) , [`--trace-token`](https://docs.cloud.google.com/sdk/gcloud/reference#--trace-token) , [`--user-output-enabled`](https://docs.cloud.google.com/sdk/gcloud/reference#--user-output-enabled) , [`--verbosity`](https://docs.cloud.google.com/sdk/gcloud/reference#--verbosity) .

Run `$ `[`gcloud help`](https://docs.cloud.google.com/sdk/gcloud/reference) for details.

NOTES

This command is currently in alpha and might change without notice. If this command fails with API permission errors despite specifying the correct project, you might be trying to access an API with an invitation-only early access allowlist.
