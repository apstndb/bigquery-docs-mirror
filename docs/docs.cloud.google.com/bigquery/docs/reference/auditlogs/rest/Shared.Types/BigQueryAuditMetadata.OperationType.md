---
name: documents/docs.cloud.google.com/bigquery/docs/reference/auditlogs/rest/Shared.Types/BigQueryAuditMetadata.OperationType
uri: https://docs.cloud.google.com/bigquery/docs/reference/auditlogs/rest/Shared.Types/BigQueryAuditMetadata.OperationType
title: BigQueryAuditMetadata.OperationType
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

Table copy job operation type.

Enums

`OPERATION_TYPE_UNSPECIFIED`

Unspecified operation type.

`COPY`

The source and the destination table have the same table type.

`SNAPSHOT`

The source table type is TABLE and the destination table type is SNAPSHOT.

`RESTORE`

The source table type is SNAPSHOT and the destination table type is TABLE.

`CLONE`

The source and the destination table have the same table type, but with a billing benefit.
