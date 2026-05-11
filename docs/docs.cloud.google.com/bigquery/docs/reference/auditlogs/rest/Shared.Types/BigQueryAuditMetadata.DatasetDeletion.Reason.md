---
name: documents/docs.cloud.google.com/bigquery/docs/reference/auditlogs/rest/Shared.Types/BigQueryAuditMetadata.DatasetDeletion.Reason
uri: https://docs.cloud.google.com/bigquery/docs/reference/auditlogs/rest/Shared.Types/BigQueryAuditMetadata.DatasetDeletion.Reason
title: BigQueryAuditMetadata.DatasetDeletion.Reason
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

Describes how the dataset was deleted.

Enums

`REASON_UNSPECIFIED`

Unknown.

`DELETE`

Dataset was deleted using the datasets.delete API.

`QUERY`

Dataset was deleted using a query job, e.g., DROP SCHEMA statement.
