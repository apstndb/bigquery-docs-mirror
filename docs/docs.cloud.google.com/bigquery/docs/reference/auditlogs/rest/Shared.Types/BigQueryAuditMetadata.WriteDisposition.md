---
name: documents/docs.cloud.google.com/bigquery/docs/reference/auditlogs/rest/Shared.Types/BigQueryAuditMetadata.WriteDisposition
uri: https://docs.cloud.google.com/bigquery/docs/reference/auditlogs/rest/Shared.Types/BigQueryAuditMetadata.WriteDisposition
title: BigQueryAuditMetadata.WriteDisposition
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

Describes whether a job should overwrite or append the existing destination table if it already exists.

Enums

`WRITE_DISPOSITION_UNSPECIFIED`

Unknown.

`WRITE_EMPTY`

This job should only be writing to empty tables.

`WRITE_TRUNCATE`

This job will truncate table data and write from the beginning. This might not preserve table metadata such as table schema, row access policy, column level policy, or column descriptions. This is the default value.

`WRITE_APPEND`

This job will append to the table.

`WRITE_TRUNCATE_DATA`

This job will truncate table data but preserve table metadata such as table schema, row access policy, column level policy, or column descriptions.
