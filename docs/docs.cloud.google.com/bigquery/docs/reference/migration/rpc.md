---
name: documents/docs.cloud.google.com/bigquery/docs/reference/migration/rpc
uri: https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc
title: BigQuery Migration API
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

The migration service, exposing apis for migration jobs operations, and agent management.

## Service: bigquerymigration.googleapis.com

The Service name `bigquerymigration.googleapis.com` is needed to create RPC client stubs.

## [`google.cloud.bigquery.migration.v2.MigrationService`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.MigrationService)

| Methods                                                                                                                                                                                                         |                                                 |
|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------|
| [`CreateMigrationWorkflow`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.MigrationService.CreateMigrationWorkflow) | Creates a migration workflow.                   |
| [`DeleteMigrationWorkflow`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.MigrationService.DeleteMigrationWorkflow) | Deletes a migration workflow by name.           |
| [`GetMigrationSubtask`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.MigrationService.GetMigrationSubtask)         | Gets a previously created migration subtask.    |
| [`GetMigrationWorkflow`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.MigrationService.GetMigrationWorkflow)       | Gets a previously created migration workflow.   |
| [`ListMigrationSubtasks`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.MigrationService.ListMigrationSubtasks)     | Lists previously created migration subtasks.    |
| [`ListMigrationWorkflows`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.MigrationService.ListMigrationWorkflows)   | Lists previously created migration workflow.    |
| [`StartMigrationWorkflow`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.MigrationService.StartMigrationWorkflow)   | Starts a previously created migration workflow. |

## [`google.cloud.bigquery.migration.v2alpha.MigrationService`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2alpha#google.cloud.bigquery.migration.v2alpha.MigrationService)

| Methods                                                                                                                                                                                                                   |                                                 |
|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------|
| [`CreateMigrationWorkflow`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2alpha#google.cloud.bigquery.migration.v2alpha.MigrationService.CreateMigrationWorkflow) | Creates a migration workflow.                   |
| [`DeleteMigrationWorkflow`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2alpha#google.cloud.bigquery.migration.v2alpha.MigrationService.DeleteMigrationWorkflow) | Deletes a migration workflow by name.           |
| [`GetMigrationSubtask`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2alpha#google.cloud.bigquery.migration.v2alpha.MigrationService.GetMigrationSubtask)         | Gets a previously created migration subtask.    |
| [`GetMigrationWorkflow`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2alpha#google.cloud.bigquery.migration.v2alpha.MigrationService.GetMigrationWorkflow)       | Gets a previously created migration workflow.   |
| [`ListMigrationSubtasks`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2alpha#google.cloud.bigquery.migration.v2alpha.MigrationService.ListMigrationSubtasks)     | Lists previously created migration subtasks.    |
| [`ListMigrationWorkflows`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2alpha#google.cloud.bigquery.migration.v2alpha.MigrationService.ListMigrationWorkflows)   | Lists previously created migration workflow.    |
| [`StartMigrationWorkflow`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2alpha#google.cloud.bigquery.migration.v2alpha.MigrationService.StartMigrationWorkflow)   | Starts a previously created migration workflow. |
