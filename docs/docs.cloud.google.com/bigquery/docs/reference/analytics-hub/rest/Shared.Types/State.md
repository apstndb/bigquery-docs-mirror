---
name: documents/docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/Shared.Types/State
uri: https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/Shared.Types/State
title: State
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

State of the subscription.

Enums

`STATE_UNSPECIFIED`

Default value. This value is unused.

`STATE_ACTIVE`

This subscription is active and the data is accessible.

`STATE_STALE`

The data referenced by this subscription is out of date and should be refreshed. This can happen when a data provider adds or removes datasets.

`STATE_INACTIVE`

This subscription has been cancelled or revoked and the data is no longer accessible.
