---
name: documents/docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/migration
uri: https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/migration
title: gcloud alpha bq migration
description: Offers tools and libraries that allow you to create and manage resources across Google Cloud.
data_source: docs.cloud.google.com
---

NAME

gcloud alpha bq migration - manage BigQuery Migration Service resources

SYNOPSIS

`gcloud alpha bq migration` [`GROUP`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/migration#GROUP) \| [`COMMAND`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/migration#COMMAND) \[ [`GCLOUD_WIDE_FLAG`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/migration#GCLOUD-WIDE-FLAGS)` …` \]

DESCRIPTION

`(ALPHA)` Manage BigQuery Migration Service resources.

GCLOUD WIDE FLAGS

These flags are available to all commands: [`--help`](https://docs.cloud.google.com/sdk/gcloud/reference#--help) .

Run `$ `[`gcloud help`](https://docs.cloud.google.com/sdk/gcloud/reference) for details.

GROUPS

`GROUP` is one of the following:

[`translation`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/migration/translation)  
`(ALPHA)` Manage BigQuery Migration Service translations.

COMMANDS

`COMMAND` is one of the following:

[`translate`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/migration/translate)  
`(ALPHA)` Translate a SQL query from a source dialect to BigQuery.

[`translate-batch`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/migration/translate-batch)  
`(ALPHA)` Translates a batch of SQL queries.

[`translate-metadata`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/migration/translate-metadata)  
`(ALPHA)` Translates metadata from zip files into DDL statements and table mappings.

REGIONAL ENDPOINTS

This command group supports regional endpoints. To use regional endpoints for this command, use the `--endpoint-mode=regional-preferred` flag. To use regional endpoints by default, run `$ `[`gcloud config set`](https://docs.cloud.google.com/sdk/gcloud/reference/config/set)` regional/endpoint_mode regional-preferred` .

NOTES

This command is currently in alpha and might change without notice. If this command fails with API permission errors despite specifying the correct project, you might be trying to access an API with an invitation-only early access allowlist.
