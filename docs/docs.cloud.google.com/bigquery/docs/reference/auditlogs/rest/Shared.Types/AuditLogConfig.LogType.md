---
name: documents/docs.cloud.google.com/bigquery/docs/reference/auditlogs/rest/Shared.Types/AuditLogConfig.LogType
uri: https://docs.cloud.google.com/bigquery/docs/reference/auditlogs/rest/Shared.Types/AuditLogConfig.LogType
title: AuditLogConfig.LogType
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

The list of valid permission types for which logging can be configured. Admin writes are always logged, and are not configurable.

Enums

`LOG_TYPE_UNSPECIFIED`

Default case. Should never be this.

`ADMIN_READ`

Admin reads. Example: CloudIAM getIamPolicy

`DATA_WRITE`

Data writes. Example: CloudSQL Users create

`DATA_READ`

Data reads. Example: CloudSQL Users list
