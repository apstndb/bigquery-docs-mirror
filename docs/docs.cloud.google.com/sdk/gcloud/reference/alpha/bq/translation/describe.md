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

`gcloud alpha bq translation describe` [`TRANSLATION_ID`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/translation/describe#TRANSLATION_ID) [`--location`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/translation/describe#--location) = `LOCATION` \[ [`GCLOUD_WIDE_FLAG`](https://docs.cloud.google.com/sdk/gcloud/reference/alpha/bq/translation/describe#GCLOUD-WIDE-FLAGS)` …` \]

EXAMPLES

To get the details of a batch translation with ID `12345678-1234-1234-1234-1234567890ab` in location `us-central1` , run:

```
gcloud alpha bq translation describe 12345678-1234-1234-1234-1234567890ab --location=us-central1
```

POSITIONAL ARGUMENTS

`TRANSLATION_ID`  
The translation ID to describe.

REQUIRED FLAGS

`--location` = `LOCATION`  
The location of the translation.

GCLOUD WIDE FLAGS

These flags are available to all commands: [`--access-token-file`](https://docs.cloud.google.com/sdk/gcloud/reference#--access-token-file) , [`--account`](https://docs.cloud.google.com/sdk/gcloud/reference#--account) , [`--billing-project`](https://docs.cloud.google.com/sdk/gcloud/reference#--billing-project) , [`--configuration`](https://docs.cloud.google.com/sdk/gcloud/reference#--configuration) , [`--flags-file`](https://docs.cloud.google.com/sdk/gcloud/reference#--flags-file) , [`--flatten`](https://docs.cloud.google.com/sdk/gcloud/reference#--flatten) , [`--format`](https://docs.cloud.google.com/sdk/gcloud/reference#--format) , [`--help`](https://docs.cloud.google.com/sdk/gcloud/reference#--help) , [`--impersonate-service-account`](https://docs.cloud.google.com/sdk/gcloud/reference#--impersonate-service-account) , [`--log-http`](https://docs.cloud.google.com/sdk/gcloud/reference#--log-http) , [`--project`](https://docs.cloud.google.com/sdk/gcloud/reference#--project) , [`--quiet`](https://docs.cloud.google.com/sdk/gcloud/reference#--quiet) , [`--trace-token`](https://docs.cloud.google.com/sdk/gcloud/reference#--trace-token) , [`--user-output-enabled`](https://docs.cloud.google.com/sdk/gcloud/reference#--user-output-enabled) , [`--verbosity`](https://docs.cloud.google.com/sdk/gcloud/reference#--verbosity) .

Run `$ `[`gcloud help`](https://docs.cloud.google.com/sdk/gcloud/reference) for details.

NOTES

This command is currently in alpha and might change without notice. If this command fails with API permission errors despite specifying the correct project, you might be trying to access an API with an invitation-only early access allowlist.
