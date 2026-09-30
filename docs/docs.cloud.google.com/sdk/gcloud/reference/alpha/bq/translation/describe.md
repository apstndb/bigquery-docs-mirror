---
name: documents/docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/translation/describe
uri: https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/translation/describe
title: gcloud alpha bq translation describe
description: Offers tools and libraries that allow you to create and manage resources across Google Cloud.
data_source: docs.cloud.google.com
---

NAME

gcloud alpha bq translation describe - get the details or status of a submitted batch translation

SYNOPSIS

`gcloud alpha bq translation describe` `  TRANSLATION_ID  ` `  --location  ` = `  LOCATION  ` \[ `  GCLOUD_WIDE_FLAG …  ` \]

EXAMPLES

To get the details of a batch translation with ID `12345678-1234-1234-1234-1234567890ab` in location `us-central1` , run:

    gcloud alpha bq translation describe 12345678-1234-1234-1234-1234567890ab --location=us-central1

POSITIONAL ARGUMENTS

  - `  TRANSLATION_ID  `  
    The translation ID to describe.

REQUIRED FLAGS

  - `--location` = `  LOCATION  `  
    The location of the translation.

GCLOUD WIDE FLAGS

These flags are available to all commands: `  --access-token-file  ` , `  --account  ` , `  --billing-project  ` , `  --configuration  ` , `  --flags-file  ` , `  --flatten  ` , `  --format  ` , `  --help  ` , `  --impersonate-service-account  ` , `  --log-http  ` , `  --project  ` , `  --quiet  ` , `  --trace-token  ` , `  --user-output-enabled  ` , `  --verbosity  ` .

Run ` $ gcloud help  ` for details.

NOTES

This command is currently in alpha and might change without notice. If this command fails with API permission errors despite specifying the correct project, you might be trying to access an API with an invitation-only early access allowlist.
