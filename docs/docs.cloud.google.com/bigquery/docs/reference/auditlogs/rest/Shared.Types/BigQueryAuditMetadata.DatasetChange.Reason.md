---
name: documents/docs.cloud.google.com/bigquery/docs/reference/auditlogs/rest/Shared.Types/BigQueryAuditMetadata.DatasetChange.Reason
uri: https://docs.cloud.google.com/bigquery/docs/reference/auditlogs/rest/Shared.Types/BigQueryAuditMetadata.DatasetChange.Reason
title: BigQueryAuditMetadata.DatasetChange.Reason
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
update_time: "2025-10-17T21:04:42Z"
---

Describes how the dataset was changed.

Enums

`REASON_UNSPECIFIED`

Unknown.

`UPDATE`

Dataset was changed using the datasets.update or datasets.patch API.

`SET_IAM_POLICY`

Dataset was changed using the SetIamPolicy API.

`QUERY`

Dataset was changed using a query job, e.g., ALTER SCHEMA statement.
