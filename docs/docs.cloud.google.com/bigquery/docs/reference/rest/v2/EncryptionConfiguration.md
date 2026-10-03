---
name: documents/docs.cloud.google.com/bigquery/docs/reference/rest/v2/EncryptionConfiguration
uri: https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/EncryptionConfiguration
title: EncryptionConfiguration
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

- [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/EncryptionConfiguration#SCHEMA_REPRESENTATION)

Configuration for Cloud KMS encryption settings.

**JSON representation**

```
{
  "kmsKeyName": string
}
```

| Fields       |                                                                                                                                                                                                                      |
|--------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `kmsKeyName` | `string` Optional. Describes the Cloud KMS encryption key that will be used to protect destination BigQuery table. The BigQuery Service Account associated with your project requires access to this encryption key. |
