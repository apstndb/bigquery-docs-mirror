---
name: documents/docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/translation
uri: https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/translation
title: gcloud alpha bq translation
description: Offers tools and libraries that allow you to create and manage resources across Google Cloud.
data_source: docs.cloud.google.com
---

NAME

gcloud alpha bq translation - manage BigQuery Migration Service translations

SYNOPSIS

`gcloud alpha bq translation` `  COMMAND  ` \[ `  GCLOUD_WIDE_FLAG …  ` \]

DESCRIPTION

`(ALPHA)` Manage BigQuery Migration Service translations.

GCLOUD WIDE FLAGS

These flags are available to all commands: `  --help  ` .

Run ` $ gcloud help  ` for details.

COMMANDS

`  COMMAND  ` is one of the following:

  - `  describe  `  
    `(ALPHA)` Get the details or status of a submitted batch translation.
  - `  generate-source-ddl  `  
    `(ALPHA)` Generates source DDL schemas from a batch of SQL queries using AI.
  - `  translate  `  
    `(ALPHA)` Translate a SQL query from a source dialect to BigQuery.
  - `  translate-batch  `  
    `(ALPHA)` Translates a batch of SQL queries.
  - `  translate-metadata  `  
    `(ALPHA)` Translates metadata from zip files into DDL statements and table mappings.

NOTES

This command is currently in alpha and might change without notice. If this command fails with API permission errors despite specifying the correct project, you might be trying to access an API with an invitation-only early access allowlist.
