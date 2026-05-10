---
name: documents/docs.cloud.google.com/bigquery/docs/reference/auditlogs/rest/Shared.Types/BigQueryAuditMetadata.TableCreation.Reason
uri: https://docs.cloud.google.com/bigquery/docs/reference/auditlogs/rest/Shared.Types/BigQueryAuditMetadata.TableCreation.Reason
title: BigQueryAuditMetadata.TableCreation.Reason
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
update_time: "2025-10-17T21:04:54Z"
---

Describes how the table was created.

Enums

`REASON_UNSPECIFIED`

Unknown.

`JOB`

Table was created as a destination table during a query, load or copy job.

`QUERY`

Table was created using a DDL query.

`TABLE_INSERT_REQUEST`

Table was created using the tables.create API.
