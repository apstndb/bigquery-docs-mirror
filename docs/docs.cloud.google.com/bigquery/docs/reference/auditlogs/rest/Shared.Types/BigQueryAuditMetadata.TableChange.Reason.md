---
name: documents/docs.cloud.google.com/bigquery/docs/reference/auditlogs/rest/Shared.Types/BigQueryAuditMetadata.TableChange.Reason
uri: https://docs.cloud.google.com/bigquery/docs/reference/auditlogs/rest/Shared.Types/BigQueryAuditMetadata.TableChange.Reason
title: BigQueryAuditMetadata.TableChange.Reason
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

Describes how the table metadata was changed.

Enums

`REASON_UNSPECIFIED`

Unknown.

`TABLE_UPDATE_REQUEST`

Table metadata was updated using the tables.update or tables.patch API.

`JOB`

Table was used as a job destination table.

`QUERY`

Table metadata was updated using a DML or DDL query.

`SET_IAM_POLICY`

Table metadata was updated using the SetIamPolicy API.
