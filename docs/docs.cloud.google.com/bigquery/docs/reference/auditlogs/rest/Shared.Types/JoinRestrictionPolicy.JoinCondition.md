---
name: documents/docs.cloud.google.com/bigquery/docs/reference/auditlogs/rest/Shared.Types/JoinRestrictionPolicy.JoinCondition
uri: https://docs.cloud.google.com/bigquery/docs/reference/auditlogs/rest/Shared.Types/JoinRestrictionPolicy.JoinCondition
title: JoinRestrictionPolicy.JoinCondition
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
update_time: "2025-10-17T21:04:49Z"
---

Enum for Join Restrictions policy.

Enums

`JOIN_CONDITION_UNSPECIFIED`

A join is neither required nor restricted on any column. Default value.

`JOIN_ANY`

A join is required on at least one of the specified columns.

`JOIN_ALL`

A join is required on all specified columns.

`JOIN_NOT_REQUIRED`

A join is not required, but if present it is only permitted on 'joinAllowedColumns'

`JOIN_BLOCKED`

Joins are blocked for all queries.
