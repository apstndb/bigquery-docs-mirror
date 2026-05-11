---
name: documents/docs.cloud.google.com/bigquery/docs/reference/migration/rest/Shared.Types/MetricKind
uri: https://docs.cloud.google.com/bigquery/docs/reference/migration/rest/Shared.Types/MetricKind
title: MetricKind
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

The kind of measurement. It describes how the data is reported. For information on setting the start time and end time based on the MetricKind, see \[TimeInterval\]\[google.monitoring.v3.TimeInterval\].

Enums

`METRIC_KIND_UNSPECIFIED`

Do not use this default value.

`GAUGE`

An instantaneous measurement of a value.

`DELTA`

The change in a value during a time interval.

`CUMULATIVE`

A value accumulated over a time interval. Cumulative measurements in a time series should have the same start time and increasing end times, until an event resets the cumulative value to zero and sets a new start time for the following points.
