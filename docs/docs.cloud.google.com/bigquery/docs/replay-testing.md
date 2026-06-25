---
name: documents/docs.cloud.google.com/bigquery/docs/replay-testing
uri: https://docs.cloud.google.com/bigquery/docs/replay-testing
title: How BigQuery uses replay testing
description: Before BigQuery introduces system updates, it proactively tests for regressions by re-running queries from production workloads.
data_source: docs.cloud.google.com
---

# How BigQuery uses replay testing

Before BigQuery introduces system updates, it tests a sample of user queries to check for regressions by re-running queries from production workloads. These background tests can help detect system updates that might compromise the accuracy or performance of existing user queries.

To achieve comprehensive coverage, BigQuery automatically selects a diverse, representative subset of queries from production workloads. If the validation detects regressions, BigQuery doesn't implement the update.

This automated validation respects data privacy. BigQuery re-runs the queries in the background without modifying your data, and the tests incur no additional cost or resource consumption. Data access logs might attribute these re-executions to the `bigquery-adminbot@system.gserviceaccount.com` account.

## What's next

  - Learn how to [run queries](https://docs.cloud.google.com/bigquery/docs/running-queries) .
  - Learn about [SQL in BigQuery](https://docs.cloud.google.com/bigquery/docs/introduction-sql) .
