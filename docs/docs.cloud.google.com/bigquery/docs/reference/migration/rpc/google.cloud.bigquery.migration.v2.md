---
name: documents/docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2
uri: https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2
title: Package google.cloud.bigquery.migration.v2
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

## Index

- [`MigrationService`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.MigrationService) (interface)
- [`AssessmentFeatureHandle`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.AssessmentFeatureHandle) (message)
- [`AssessmentTaskDetails`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.AssessmentTaskDetails) (message)
- [`AzureSynapseDialect`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.AzureSynapseDialect) (message)
- [`BigQueryDialect`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.BigQueryDialect) (message)
- [`CreateMigrationWorkflowRequest`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.CreateMigrationWorkflowRequest) (message)
- [`DB2Dialect`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.DB2Dialect) (message)
- [`DeleteMigrationWorkflowRequest`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.DeleteMigrationWorkflowRequest) (message)
- [`Dialect`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.Dialect) (message)
- [`ErrorDetail`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.ErrorDetail) (message)
- [`ErrorLocation`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.ErrorLocation) (message)
- [`GcsReportLogMessage`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.GcsReportLogMessage) (message)
- [`GetMigrationSubtaskRequest`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.GetMigrationSubtaskRequest) (message)
- [`GetMigrationWorkflowRequest`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.GetMigrationWorkflowRequest) (message)
- [`GreenplumDialect`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.GreenplumDialect) (message)
- [`HiveQLDialect`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.HiveQLDialect) (message)
- [`LineageOutput`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.LineageOutput) (message)
- [`LineageOutput.ProgressReport`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.LineageOutput.ProgressReport) (message)
- [`LineageOutput.ProgressReport.ProcessingStage`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.LineageOutput.ProgressReport.ProcessingStage) (enum)
- [`LineageOutput.ProgressReport.WorkSummary`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.LineageOutput.ProgressReport.WorkSummary) (message)
- [`LineageOutput.ProgressReport.WorkSummary.State`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.LineageOutput.ProgressReport.WorkSummary.State) (enum)
- [`LineageOutput.RecognizedInput`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.LineageOutput.RecognizedInput) (message)
- [`LineageOutput.RecognizedInput.Type`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.LineageOutput.RecognizedInput.Type) (enum)
- [`ListMigrationSubtasksRequest`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.ListMigrationSubtasksRequest) (message)
- [`ListMigrationSubtasksResponse`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.ListMigrationSubtasksResponse) (message)
- [`ListMigrationWorkflowsRequest`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.ListMigrationWorkflowsRequest) (message)
- [`ListMigrationWorkflowsResponse`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.ListMigrationWorkflowsResponse) (message)
- [`Literal`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.Literal) (message)
- [`MigrationSubtask`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.MigrationSubtask) (message)
- [`MigrationSubtask.State`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.MigrationSubtask.State) (enum)
- [`MigrationTask`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.MigrationTask) (message)
- [`MigrationTask.State`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.MigrationTask.State) (enum)
- [`MigrationTaskResult`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.MigrationTaskResult) (message)
- [`MigrationWorkflow`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.MigrationWorkflow) (message)
- [`MigrationWorkflow.State`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.MigrationWorkflow.State) (enum)
- [`MySQLDialect`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.MySQLDialect) (message)
- [`NameMappingKey`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.NameMappingKey) (message)
- [`NameMappingKey.Type`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.NameMappingKey.Type) (enum)
- [`NameMappingValue`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.NameMappingValue) (message)
- [`NetezzaDialect`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.NetezzaDialect) (message)
- [`ObjectNameMapping`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.ObjectNameMapping) (message)
- [`ObjectNameMappingList`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.ObjectNameMappingList) (message)
- [`OracleDialect`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.OracleDialect) (message)
- [`Point`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.Point) (message)
- [`PostgresqlDialect`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.PostgresqlDialect) (message)
- [`PrestoDialect`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.PrestoDialect) (message)
- [`RedshiftDialect`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.RedshiftDialect) (message)
- [`ResourceErrorDetail`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.ResourceErrorDetail) (message)
- [`SQLServerDialect`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.SQLServerDialect) (message)
- [`SQLiteDialect`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.SQLiteDialect) (message)
- [`SnowflakeDialect`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.SnowflakeDialect) (message)
- [`SourceEnv`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.SourceEnv) (message)
- [`SourceEnvironment`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.SourceEnvironment) (message)
- [`SourceSpec`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.SourceSpec) (message)
- [`SourceTargetMapping`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.SourceTargetMapping) (message)
- [`SparkSQLDialect`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.SparkSQLDialect) (message)
- [`StartMigrationWorkflowRequest`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.StartMigrationWorkflowRequest) (message)
- [`SuggestionConfig`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.SuggestionConfig) (message)
- [`SuggestionStep`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.SuggestionStep) (message)
- [`SuggestionStep.RewriteTarget`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.SuggestionStep.RewriteTarget) (enum)
- [`SuggestionStep.SuggestionType`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.SuggestionStep.SuggestionType) (enum)
- [`TargetSpec`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.TargetSpec) (message)
- [`TaskOutput`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.TaskOutput) (message)
- [`TaskOutput.State`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.TaskOutput.State) (enum)
- [`TeradataDialect`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.TeradataDialect) (message)
- [`TeradataDialect.Mode`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.TeradataDialect.Mode) (enum)
- [`TimeInterval`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.TimeInterval) (message)
- [`TimeSeries`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.TimeSeries) (message)
- [`TranslationConfigDetails`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.TranslationConfigDetails) (message)
- [`TranslationDetails`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.TranslationDetails) (message)
- [`TranslationTaskResult`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.TranslationTaskResult) (message)
- [`TypedValue`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.TypedValue) (message)
- [`VerticaDialect`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.VerticaDialect) (message)

## MigrationService

Service to handle EDW migrations.

**CreateMigrationWorkflow**

`rpc CreateMigrationWorkflow( `[`CreateMigrationWorkflowRequest`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.CreateMigrationWorkflowRequest)` ) returns ( `[`MigrationWorkflow`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.MigrationWorkflow)` )`

Creates a migration workflow.

Authorization scopes  
Requires the following OAuth scope:

- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

<!-- -->

IAM Permissions  
Requires the following [IAM](https://cloud.google.com/iam/docs) permission on the `parent` resource:

- `bigquerymigration.workflows.create`

For more information, see the [IAM documentation](https://cloud.google.com/iam/docs) .

**DeleteMigrationWorkflow**

`rpc DeleteMigrationWorkflow( `[`DeleteMigrationWorkflowRequest`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.DeleteMigrationWorkflowRequest)` ) returns ( `[`Empty`](https://protobuf.dev/reference/protobuf/google.protobuf/#empty)` )`

Deletes a migration workflow by name.

Authorization scopes  
Requires the following OAuth scope:

- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

<!-- -->

IAM Permissions  
Requires the following [IAM](https://cloud.google.com/iam/docs) permission on the `name` resource:

- `bigquerymigration.workflows.delete`

For more information, see the [IAM documentation](https://cloud.google.com/iam/docs) .

**GetMigrationSubtask**

`rpc GetMigrationSubtask( `[`GetMigrationSubtaskRequest`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.GetMigrationSubtaskRequest)` ) returns ( `[`MigrationSubtask`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.MigrationSubtask)` )`

Gets a previously created migration subtask.

Authorization scopes  
Requires the following OAuth scope:

- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

<!-- -->

IAM Permissions  
Requires the following [IAM](https://cloud.google.com/iam/docs) permission on the `name` resource:

- `bigquerymigration.subtasks.get`

For more information, see the [IAM documentation](https://cloud.google.com/iam/docs) .

**GetMigrationWorkflow**

`rpc GetMigrationWorkflow( `[`GetMigrationWorkflowRequest`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.GetMigrationWorkflowRequest)` ) returns ( `[`MigrationWorkflow`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.MigrationWorkflow)` )`

Gets a previously created migration workflow.

Authorization scopes  
Requires the following OAuth scope:

- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

<!-- -->

IAM Permissions  
Requires the following [IAM](https://cloud.google.com/iam/docs) permission on the `name` resource:

- `bigquerymigration.workflows.get`

For more information, see the [IAM documentation](https://cloud.google.com/iam/docs) .

**ListMigrationSubtasks**

`rpc ListMigrationSubtasks( `[`ListMigrationSubtasksRequest`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.ListMigrationSubtasksRequest)` ) returns ( `[`ListMigrationSubtasksResponse`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.ListMigrationSubtasksResponse)` )`

Lists previously created migration subtasks.

Authorization scopes  
Requires the following OAuth scope:

- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

<!-- -->

IAM Permissions  
Requires the following [IAM](https://cloud.google.com/iam/docs) permission on the `parent` resource:

- `bigquerymigration.subtasks.list`

For more information, see the [IAM documentation](https://cloud.google.com/iam/docs) .

**ListMigrationWorkflows**

`rpc ListMigrationWorkflows( `[`ListMigrationWorkflowsRequest`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.ListMigrationWorkflowsRequest)` ) returns ( `[`ListMigrationWorkflowsResponse`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.ListMigrationWorkflowsResponse)` )`

Lists previously created migration workflow.

Authorization scopes  
Requires the following OAuth scope:

- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

<!-- -->

IAM Permissions  
Requires the following [IAM](https://cloud.google.com/iam/docs) permission on the `parent` resource:

- `bigquerymigration.workflows.list`

For more information, see the [IAM documentation](https://cloud.google.com/iam/docs) .

**StartMigrationWorkflow**

`rpc StartMigrationWorkflow( `[`StartMigrationWorkflowRequest`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.StartMigrationWorkflowRequest)` ) returns ( `[`Empty`](https://protobuf.dev/reference/protobuf/google.protobuf/#empty)` )`

Starts a previously created migration workflow. I.e., the state transitions from DRAFT to RUNNING. This is a no-op if the state is already RUNNING. An error will be signaled if the state is anything other than DRAFT or RUNNING.

Authorization scopes  
Requires the following OAuth scope:

- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

<!-- -->

IAM Permissions  
Requires the following [IAM](https://cloud.google.com/iam/docs) permission on the `name` resource:

- `bigquerymigration.workflows.update`

For more information, see the [IAM documentation](https://cloud.google.com/iam/docs) .

## AssessmentFeatureHandle

User-definable feature flags for assessment tasks.

| Fields                  |                                                                                                         |
|-------------------------|---------------------------------------------------------------------------------------------------------|
| `add_shareable_dataset` | `bool` Optional. Whether to create a dataset containing non-PII data in addition to the output dataset. |
| `generate_tco_report`   | `bool` Optional. Whether the TCO report Google Doc generation is allowlisted for the project.           |

## AssessmentTaskDetails

Assessment task config.

| Fields           |                                                                                                                                                                                                                                                                        |
|------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `input_path`     | `string` Required. The Cloud Storage path for assessment input files.                                                                                                                                                                                                  |
| `output_dataset` | `string` Required. The BigQuery dataset for output.                                                                                                                                                                                                                    |
| `querylogs_path` | `string` Optional. An optional Cloud Storage path to write the query logs (which is then used as an input path on the translation task)                                                                                                                                |
| `data_source`    | `string` Required. The data source or data warehouse type (eg: TERADATA/REDSHIFT) from which the input data is extracted.                                                                                                                                              |
| `feature_handle` | [`AssessmentFeatureHandle`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.AssessmentFeatureHandle) Optional. A collection of additional feature flags for this assessment. |

## AzureSynapseDialect

This type has no fields.

The dialect definition for Azure Synapse.

## BigQueryDialect

This type has no fields.

The dialect definition for BigQuery.

## CreateMigrationWorkflowRequest

Request to create a migration workflow resource.

| Fields               |                                                                                                                                                                                                                                |
|----------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `parent`             | `string` Required. The name of the project to which this migration workflow belongs. Example: `projects/foo/locations/bar`                                                                                                     |
| `migration_workflow` | [`MigrationWorkflow`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.MigrationWorkflow) Required. The migration workflow to create. |

## DB2Dialect

This type has no fields.

The dialect definition for DB2.

## DeleteMigrationWorkflowRequest

A request to delete a previously created migration workflow.

| Fields |                                                                                                                          |
|--------|--------------------------------------------------------------------------------------------------------------------------|
| `name` | `string` Required. The unique identifier for the migration workflow. Example: `projects/123/locations/us/workflows/1234` |

## Dialect

The possible dialect options for translation.

| Fields                                                                                                                                     |                                                                                                                                                                                                                  |
|--------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `dialect_value` . The possible dialect options that this message represents. `dialect_value` can be only one of the following: |                                                                                                                                                                                                                  |
| `bigquery_dialect`                                                                                                                         | [`BigQueryDialect`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.BigQueryDialect) The BigQuery dialect              |
| `hiveql_dialect`                                                                                                                           | [`HiveQLDialect`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.HiveQLDialect) The HiveQL dialect                    |
| `redshift_dialect`                                                                                                                         | [`RedshiftDialect`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.RedshiftDialect) The Redshift dialect              |
| `teradata_dialect`                                                                                                                         | [`TeradataDialect`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.TeradataDialect) The Teradata dialect              |
| `oracle_dialect`                                                                                                                           | [`OracleDialect`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.OracleDialect) The Oracle dialect                    |
| `sparksql_dialect`                                                                                                                         | [`SparkSQLDialect`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.SparkSQLDialect) The SparkSQL dialect              |
| `snowflake_dialect`                                                                                                                        | [`SnowflakeDialect`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.SnowflakeDialect) The Snowflake dialect           |
| `netezza_dialect`                                                                                                                          | [`NetezzaDialect`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.NetezzaDialect) The Netezza dialect                 |
| `azure_synapse_dialect`                                                                                                                    | [`AzureSynapseDialect`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.AzureSynapseDialect) The Azure Synapse dialect |
| `vertica_dialect`                                                                                                                          | [`VerticaDialect`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.VerticaDialect) The Vertica dialect                 |
| `sql_server_dialect`                                                                                                                       | [`SQLServerDialect`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.SQLServerDialect) The SQL Server dialect          |
| `postgresql_dialect`                                                                                                                       | [`PostgresqlDialect`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.PostgresqlDialect) The Postgresql dialect        |
| `presto_dialect`                                                                                                                           | [`PrestoDialect`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.PrestoDialect) The Presto dialect                    |
| `mysql_dialect`                                                                                                                            | [`MySQLDialect`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.MySQLDialect) The MySQL dialect                       |
| `db2_dialect`                                                                                                                              | [`DB2Dialect`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.DB2Dialect) DB2 dialect                                 |
| `sqlite_dialect`                                                                                                                           | [`SQLiteDialect`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.SQLiteDialect) SQLite dialect                        |
| `greenplum_dialect`                                                                                                                        | [`GreenplumDialect`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.GreenplumDialect) Greenplum dialect               |

## ErrorDetail

Provides details for errors, e.g. issues that where encountered when processing a subtask.

| Fields       |                                                                                                                                                                                                                                              |
|--------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `location`   | [`ErrorLocation`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.ErrorLocation) Optional. The exact location within the resource (if applicable). |
| `error_info` | [`ErrorInfo`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.rpc#google.rpc.ErrorInfo) Required. Describes the cause of the error with structured detail.                                                        |

## ErrorLocation

Holds information about where the error is located.

| Fields   |                                                                                                                                        |
|----------|----------------------------------------------------------------------------------------------------------------------------------------|
| `line`   | `int32` Optional. If applicable, denotes the line where the error occurred. A zero value means that there is no line information.      |
| `column` | `int32` Optional. If applicable, denotes the column where the error occurred. A zero value means that there is no columns information. |

## GcsReportLogMessage

A record in the aggregate CSV report for a migration workflow

| Fields                 |                                                                                                                                            |
|------------------------|--------------------------------------------------------------------------------------------------------------------------------------------|
| `severity`             | `string` Severity of the translation record.                                                                                               |
| `category`             | `string` Category of the error/warning. Example: SyntaxError                                                                               |
| `file_path`            | `string` The file path in which the error occurred                                                                                         |
| `filename`             | `string` The file name in which the error occurred                                                                                         |
| `source_script_line`   | `int32` Specifies the row from the source text where the error occurred (0 based, -1 for messages without line location). Example: 2       |
| `source_script_column` | `int32` Specifies the column from the source texts where the error occurred. (0 based, -1 for messages without column location) example: 6 |
| `message`              | `string` Detailed message of the record.                                                                                                   |
| `script_context`       | `string` The script context (obfuscated) in which the error occurred                                                                       |
| `action`               | `string` Category of the error/warning. Example: SyntaxError                                                                               |
| `effect`               | `string` Effect of the error/warning. Example: COMPATIBILITY                                                                               |
| `object_name`          | `string` Name of the affected object in the log message.                                                                                   |

## GetMigrationSubtaskRequest

A request to get a previously created migration subtasks.

| Fields      |                                                                                                                                      |
|-------------|--------------------------------------------------------------------------------------------------------------------------------------|
| `name`      | `string` Required. The unique identifier for the migration subtask. Example: `projects/123/locations/us/workflows/1234/subtasks/543` |
| `read_mask` | [`FieldMask`](https://protobuf.dev/reference/protobuf/google.protobuf/#field-mask) Optional. The list of fields to be retrieved.     |

## GetMigrationWorkflowRequest

A request to get a previously created migration workflow.

| Fields      |                                                                                                                          |
|-------------|--------------------------------------------------------------------------------------------------------------------------|
| `name`      | `string` Required. The unique identifier for the migration workflow. Example: `projects/123/locations/us/workflows/1234` |
| `read_mask` | [`FieldMask`](https://protobuf.dev/reference/protobuf/google.protobuf/#field-mask) The list of fields to be retrieved.   |

## GreenplumDialect

This type has no fields.

The dialect definition for Greenplum.

## HiveQLDialect

This type has no fields.

The dialect definition for HiveQL.

## LineageOutput

The output of a task with output type "LINEAGE".

Actual generated lineage can be queried separately (see [`webapp_uri`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.LineageOutput.FIELDS.string.google.cloud.bigquery.migration.v2.LineageOutput.webapp_uri) ), this message contains only metadata: processing status, errors, etc.

| Fields                          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
|---------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `webapp_uri`                    | `string` The URI of the webapp that visualizes the lineage. The user needs the `bigquerymigration.googleapis.com/lineageDbs.query` IAM permission to use the webapp.                                                                                                                                                                                                                                                                                                                    |
| `recognized_inputs[]`           | [`RecognizedInput`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.LineageOutput.RecognizedInput) Output only. Recognized lineage inputs. All inputs are processed only if the task succeeds and all work is in state `SUCCEEDED` (in particular, nothing is `SKIPPED` ). Even with all inputs processed successfully, there may be transpiler errors present leading to inaccurate lineage. |
| `processing_progress_reports[]` | [`ProgressReport`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.LineageOutput.ProgressReport) Output only. Work processing progress reports broken up by processing stage.                                                                                                                                                                                                                 |

## ProgressReport

Breaks down processing progress of work.

| Fields             |                                                                                                                                                                                                                                                                                                                                                                                                                              |
|--------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `processing_stage` | [`ProcessingStage`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.LineageOutput.ProgressReport.ProcessingStage) Output only. The processing stage this progress report describes.                                                                                                                                                |
| `work_summaries[]` | [`WorkSummary`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.LineageOutput.ProgressReport.WorkSummary) Output only. Summaries of work broken up by the state of the work. Each work summary describes how much work is in the given state. To get numbers for the total work covered, aggregate the numbers from all summaries. |

## ProcessingStage

The processing stage the progress report describes.

| Enums                          |                                      |
|--------------------------------|--------------------------------------|
| `PROCESSING_STAGE_UNSPECIFIED` | The stage is not specified.          |
| `INPUT_INGESTION`              | The input ingestion stage.           |
| `POSTPROCESSING`               | The lineage DB postprocessing stage. |

## WorkSummary

Summary of work in the given state.

| Fields    |                                                                                                                                                                                                                                                                |
|-----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `state`   | [`State`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.LineageOutput.ProgressReport.WorkSummary.State) Output only. The state of the work this summary describes. |
| `size`    | `int64` Output only. Size of the work in the given State. Size counts "units of work". Units represent arbitrary division of work; there's no expectation each unit takes similar time to process.                                                             |
| `comment` | `string` Output only. Human-readable comment.                                                                                                                                                                                                                  |

## State

States of work. Each piece of work is in exactly one state. \[SUCCEEDED\], \[FAILED\] and \[SKIPPED\] are terminal states; work in the \[IN_PROGRESS\] will eventually transition to one of the terminal states.

| Enums               |                                                                                                          |
|---------------------|----------------------------------------------------------------------------------------------------------|
| `STATE_UNSPECIFIED` | The state is not specified.                                                                              |
| `SUCCEEDED`         | Work that was processed successfully.                                                                    |
| `FAILED`            | Work that failed processing.                                                                             |
| `IN_PROGRESS`       | Work that is currently being processed or queued for processing.                                         |
| `SKIPPED`           | Work that was recognised as necessary to fully process inputs but was skipped due to system limitations. |

## RecognizedInput

Information about lineage input of the given type that lineage generation recognized.

If you expected to process more of the given input, verify your input was uploaded and is in the correct format and the request to generate lineage correctly specified the input location.

| Fields                    |                                                                                                                                                                                                                            |
|---------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `type`                    | [`Type`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.LineageOutput.RecognizedInput.Type) Output only. The type of the input. |
| `uncompressed_size_bytes` | `int64` Output only. The uncompressed size of the recognized input of the given type.                                                                                                                                      |

## Type

Input type recognized by the lineage processing.

| Enums              |                            |
|--------------------|----------------------------|
| `TYPE_UNSPECIFIED` | The type is not specified. |
| `METADATA`         | The input is metadata.     |
| `QUERY_LOG`        | The input is a query log.  |
| `SCRIPT`           | The input is a SQL script. |

## ListMigrationSubtasksRequest

A request to list previously created migration subtasks.

| Fields       |                                                                                                                                                                                                                                                                 |
|--------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `parent`     | `string` Required. The migration task of the subtasks to list. Example: `projects/123/locations/us/workflows/1234`                                                                                                                                              |
| `read_mask`  | [`FieldMask`](https://protobuf.dev/reference/protobuf/google.protobuf/#field-mask) Optional. The list of fields to be retrieved.                                                                                                                                |
| `page_size`  | `int32` Optional. The maximum number of migration tasks to return. The service may return fewer than this number.                                                                                                                                               |
| `page_token` | `string` Optional. A page token, received from previous `ListMigrationSubtasks` call. Provide this to retrieve the subsequent page. When paginating, all other parameters provided to `ListMigrationSubtasks` must match the call that provided the page token. |
| `filter`     | `string` Optional. The filter to apply. This can be used to get the subtasks of a specific tasks in a workflow, e.g. `migration_task = "ab012"` where `"ab012"` is the task ID (not the name in the named map).                                                 |

## ListMigrationSubtasksResponse

Response object for a `ListMigrationSubtasks` call.

| Fields                 |                                                                                                                                                                                                                                 |
|------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `migration_subtasks[]` | [`MigrationSubtask`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.MigrationSubtask) The migration subtasks for the specified task. |
| `next_page_token`      | `string` A token, which can be sent as `page_token` to retrieve the next page. If this field is omitted, there are no subsequent pages.                                                                                         |

## ListMigrationWorkflowsRequest

A request to list previously created migration workflows.

| Fields       |                                                                                                                                                                                                                                                         |
|--------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `parent`     | `string` Required. The project and location of the migration workflows to list. Example: `projects/123/locations/us`                                                                                                                                    |
| `read_mask`  | [`FieldMask`](https://protobuf.dev/reference/protobuf/google.protobuf/#field-mask) The list of fields to be retrieved.                                                                                                                                  |
| `page_size`  | `int32` The maximum number of migration workflows to return. The service may return fewer than this number.                                                                                                                                             |
| `page_token` | `string` A page token, received from previous `ListMigrationWorkflows` call. Provide this to retrieve the subsequent page. When paginating, all other parameters provided to `ListMigrationWorkflows` must match the call that provided the page token. |

## ListMigrationWorkflowsResponse

Response object for a `ListMigrationWorkflows` call.

| Fields                  |                                                                                                                                                                                                                                                  |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `migration_workflows[]` | [`MigrationWorkflow`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.MigrationWorkflow) The migration workflows for the specified project / location. |
| `next_page_token`       | `string` A token, which can be sent as `page_token` to retrieve the next page. If this field is omitted, there are no subsequent pages.                                                                                                          |

## Literal

Literal data.

| Fields                                                                                                  |                                                         |
|---------------------------------------------------------------------------------------------------------|---------------------------------------------------------|
| `relative_path`                                                                                         | `string` Required. The identifier of the literal entry. |
| Union field `literal_data` . The literal SQL contents. `literal_data` can be only one of the following: |                                                         |
| `literal_string`                                                                                        | `string` Literal string data.                           |
| `literal_bytes`                                                                                         | `bytes` Literal byte data.                              |

## MigrationSubtask

A subtask for a migration which carries details about the configuration of the subtask. The content of the details should not matter to the end user, but is a contract between the subtask creator and subtask worker.

| Fields                     |                                                                                                                                                                                                                                                                                                                                                      |
|----------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`                     | `string` Output only. Immutable. The resource name for the migration subtask. The ID is server-generated. Example: `projects/123/locations/us/workflows/345/subtasks/678`                                                                                                                                                                            |
| `task_id`                  | `string` The unique ID of the task to which this subtask belongs.                                                                                                                                                                                                                                                                                    |
| `type`                     | `string` The type of the Subtask. The migration service does not check whether this is a known type. It is up to the task creator (i.e. orchestrator or worker) to ensure it only creates subtasks for which there are compatible workers polling for Subtasks.                                                                                      |
| `state`                    | [`State`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.MigrationSubtask.State) Output only. The current state of the subtask.                                                                                                                           |
| `processing_error`         | [`ErrorInfo`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.rpc#google.rpc.ErrorInfo) Output only. An explanation that may be populated when the task is in FAILED state.                                                                                                                                               |
| `resource_error_details[]` | [`ResourceErrorDetail`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.ResourceErrorDetail) Output only. Provides details to errors and issues encountered while processing the subtask. Presence of error details does not mean that the subtask failed. |
| `resource_error_count`     | `int32` Output only. The number or resources with errors. Note: This is not the total number of errors as each resource can have more than one error. This is used to indicate truncation by having a `resource_error_count` that is higher than the size of `resource_error_details` .                                                              |
| `create_time`              | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) Output only. Time when the subtask was created.                                                                                                                                                                                                                    |
| `last_update_time`         | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) Output only. Time when the subtask was last updated.                                                                                                                                                                                                               |
| `metrics[]`                | [`TimeSeries`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.TimeSeries) Output only. The metrics for the subtask.                                                                                                                                       |

## State

Possible states of a migration subtask.

| Enums                |                                                                                                                                                    |
|----------------------|----------------------------------------------------------------------------------------------------------------------------------------------------|
| `STATE_UNSPECIFIED`  | The state is unspecified.                                                                                                                          |
| `ACTIVE`             | The subtask is ready, i.e. it is ready for execution.                                                                                              |
| `RUNNING`            | The subtask is running, i.e. it is assigned to a worker for execution.                                                                             |
| `SUCCEEDED`          | The subtask finished successfully.                                                                                                                 |
| `FAILED`             | The subtask finished unsuccessfully.                                                                                                               |
| `PAUSED`             | The subtask is paused, i.e., it will not be scheduled. If it was already assigned,it might still finish but no new lease renewals will be granted. |
| `PENDING_DEPENDENCY` | The subtask is pending a dependency. It will be scheduled once its dependencies are done.                                                          |

## MigrationTask

A single task for a migration which has details about the configuration of the task.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>id</code></td>
<td><p><code>string</code></p>
<p>Output only. Immutable. The unique identifier for the migration task. The ID is server-generated.</p></td>
</tr>
<tr class="even">
<td><code>type</code></td>
<td><p><code>string</code></p>
<p>The type of the task. This must be one of the supported task types.</p>
<p>Assessment:</p>
<ul>
<li><code>Assessment_Hive</code> - Assessment for Hive.</li>
<li><code>Assessment_Redshift</code> - Assessment for Redshift.</li>
<li><code>Assessment_Snowflake</code> - Assessment for Snowflake.</li>
<li><code>Assessment_Teradata_v2</code> - Assessment for Teradata.</li>
<li><code>Assessment_Oracle</code> - Assessment for Oracle.</li>
<li><code>Assessment_Hadoop</code> - Assessment for Hadoop.</li>
<li><code>Assessment_Informatica</code> - Assessment for Informatica.</li>
</ul>
<p>Translation: See <a href="https://docs.cloud.google.com/bigquery/docs/api-sql-translator#supported_task_types">Supported Task Types</a> for a list of supported task types.</p></td>
</tr>
<tr class="odd">
<td><code>state</code></td>
<td><p><a href="https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.MigrationTask.State"><code>State</code></a></p>
<p>Output only. The current state of the task.</p></td>
</tr>
<tr class="even">
<td><code>processing_error</code></td>
<td><p><a href="https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.rpc#google.rpc.ErrorInfo"><code>ErrorInfo</code></a></p>
<p>Output only. An explanation that may be populated when the task is in FAILED state.</p></td>
</tr>
<tr class="odd">
<td><code>create_time</code></td>
<td><p><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp"><code>Timestamp</code></a></p>
<p>Output only. Time when the task was created.</p></td>
</tr>
<tr class="even">
<td><code>last_update_time</code></td>
<td><p><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp"><code>Timestamp</code></a></p>
<p>Output only. Time when the task was last updated.</p></td>
</tr>
<tr class="odd">
<td><code>resource_error_details[]</code></td>
<td><p><a href="https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.ResourceErrorDetail"><code>ResourceErrorDetail</code></a></p>
<p>Output only. Provides details to errors and issues encountered while processing the task. Presence of error details does not mean that the task failed.</p></td>
</tr>
<tr class="even">
<td><code>resource_error_count</code></td>
<td><p><code>int32</code></p>
<p>Output only. The number or resources with errors. Note: This is not the total number of errors as each resource can have more than one error. This is used to indicate truncation by having a <code>resource_error_count</code> that is higher than the size of <code>resource_error_details</code> .</p></td>
</tr>
<tr class="odd">
<td><code>metrics[]</code></td>
<td><p><a href="https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.TimeSeries"><code>TimeSeries</code></a></p>
<p>Output only. The metrics for the task.</p></td>
</tr>
<tr class="even">
<td><code>task_result</code></td>
<td><p><a href="https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.MigrationTaskResult"><code>MigrationTaskResult</code></a></p>
<p>Output only. The result of the task.</p></td>
</tr>
<tr class="odd">
<td><code>total_processing_error_count</code></td>
<td><p><code>int32</code></p>
<p>Output only. Count of all the processing errors in this task and its subtasks.</p></td>
</tr>
<tr class="even">
<td><code>total_resource_error_count</code></td>
<td><p><code>int32</code></p>
<p>Output only. Count of all the resource errors in this task and its subtasks.</p></td>
</tr>
<tr class="odd">
<td>Union field <code>task_details</code> . The details of the task. <code>task_details</code> can be only one of the following:</td>
<td></td>
</tr>
<tr class="even">
<td><code>assessment_task_details</code></td>
<td><p><a href="https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.AssessmentTaskDetails"><code>AssessmentTaskDetails</code></a></p>
<p>Task configuration for Assessment.</p></td>
</tr>
<tr class="odd">
<td><code>translation_config_details</code></td>
<td><p><a href="https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.TranslationConfigDetails"><code>TranslationConfigDetails</code></a></p>
<p>Task configuration for CW Batch/Offline SQL Translation.</p></td>
</tr>
<tr class="even">
<td><code>translation_details</code></td>
<td><p><a href="https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.TranslationDetails"><code>TranslationDetails</code></a></p>
<p>Task details for unified SQL Translation.</p></td>
</tr>
</tbody>
</table>

## State

Possible states of a migration task.

| Enums               |                                                                                            |
|---------------------|--------------------------------------------------------------------------------------------|
| `STATE_UNSPECIFIED` | The state is unspecified.                                                                  |
| `PENDING`           | The task is waiting for orchestration.                                                     |
| `ORCHESTRATING`     | The task is assigned to an orchestrator.                                                   |
| `RUNNING`           | The task is running, i.e. its subtasks are ready for execution.                            |
| `PAUSED`            | The task is paused. Assigned subtasks can continue, but no new subtasks will be scheduled. |
| `SUCCEEDED`         | The task finished successfully.                                                            |
| `FAILED`            | The task finished unsuccessfully.                                                          |

## MigrationTaskResult

The migration task result.

| Fields                                                                                                 |                                                                                                                                                                                                                                                          |
|--------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `task_outputs`                                                                                         | `map<string, `[`TaskOutput`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.TaskOutput)` >` The map of task output types to the task outputs, e.g. "LINEAGE". |
| Union field `details` . Details specific to the task type. `details` can be only one of the following: |                                                                                                                                                                                                                                                          |
| `translation_task_result`                                                                              | [`TranslationTaskResult`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.TranslationTaskResult) Details specific to translation task types.                   |

## MigrationWorkflow

A migration workflow which specifies what needs to be done for an EDW migration.

| Fields             |                                                                                                                                                                                                                                                                                                                                                  |
|--------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`             | `string` Output only. Immutable. Identifier. The unique identifier for the migration workflow. The ID is server-generated. Example: `projects/123/locations/us/workflows/345`                                                                                                                                                                    |
| `display_name`     | `string` The display name of the workflow. This can be set to give a workflow a descriptive name. There is no guarantee or enforcement of uniqueness.                                                                                                                                                                                            |
| `tasks`            | `map<string, `[`MigrationTask`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.MigrationTask)` >` The tasks in a workflow in a named map. The name (i.e. key) has no meaning and is merely a convenient way to address a specific task in a workflow. |
| `state`            | [`State`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.MigrationWorkflow.State) Output only. That status of the workflow.                                                                                                                           |
| `create_time`      | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) Output only. Time when the workflow was created.                                                                                                                                                                                                               |
| `last_update_time` | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) Output only. Time when the workflow was last updated.                                                                                                                                                                                                          |

## State

Possible migration workflow states.

| Enums               |                                                                                                                                                    |
|---------------------|----------------------------------------------------------------------------------------------------------------------------------------------------|
| `STATE_UNSPECIFIED` | Workflow state is unspecified.                                                                                                                     |
| `DRAFT`             | Workflow is in draft status, i.e. tasks are not yet eligible for execution.                                                                        |
| `RUNNING`           | Workflow is running (i.e. tasks are eligible for execution).                                                                                       |
| `PAUSED`            | Workflow is paused. Tasks currently in progress may continue, but no further tasks will be scheduled.                                              |
| `COMPLETED`         | Workflow is complete. There should not be any task in a non-terminal state, but if they are (e.g. forced termination), they will not be scheduled. |

## MySQLDialect

This type has no fields.

The dialect definition for MySQL.

## NameMappingKey

The potential components of a full name mapping that will be mapped during translation in the source data warehouse.

| Fields      |                                                                                                                                                                                                                  |
|-------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `type`      | [`Type`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.NameMappingKey.Type) The type of object that is being mapped. |
| `database`  | `string` The database name (BigQuery project ID equivalent in the source data warehouse).                                                                                                                        |
| `schema`    | `string` The schema name (BigQuery dataset equivalent in the source data warehouse).                                                                                                                             |
| `relation`  | `string` The relation name (BigQuery table or view equivalent in the source data warehouse).                                                                                                                     |
| `attribute` | `string` The attribute name (BigQuery column equivalent in the source data warehouse).                                                                                                                           |

## Type

The type of the object that is being mapped.

| Enums              |                                                  |
|--------------------|--------------------------------------------------|
| `TYPE_UNSPECIFIED` | Unspecified name mapping type.                   |
| `DATABASE`         | The object being mapped is a database.           |
| `SCHEMA`           | The object being mapped is a schema.             |
| `RELATION`         | The object being mapped is a relation.           |
| `ATTRIBUTE`        | The object being mapped is an attribute.         |
| `RELATION_ALIAS`   | The object being mapped is a relation alias.     |
| `ATTRIBUTE_ALIAS`  | The object being mapped is a an attribute alias. |
| `FUNCTION`         | The object being mapped is a function.           |

## NameMappingValue

The potential components of a full name mapping that will be mapped during translation in the target data warehouse.

| Fields      |                                                                                              |
|-------------|----------------------------------------------------------------------------------------------|
| `database`  | `string` The database name (BigQuery project ID equivalent in the target data warehouse).    |
| `schema`    | `string` The schema name (BigQuery dataset equivalent in the target data warehouse).         |
| `relation`  | `string` The relation name (BigQuery table or view equivalent in the target data warehouse). |
| `attribute` | `string` The attribute name (BigQuery column equivalent in the target data warehouse).       |

## NetezzaDialect

This type has no fields.

The dialect definition for Netezza.

## ObjectNameMapping

Represents a key-value pair of NameMappingKey to NameMappingValue to represent the mapping of SQL names from the input value to desired output.

| Fields   |                                                                                                                                                                                                                                              |
|----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `source` | [`NameMappingKey`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.NameMappingKey) The name of the object in source that is being mapped.          |
| `target` | [`NameMappingValue`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.NameMappingValue) The desired target name of the object that is being mapped. |

## ObjectNameMappingList

Represents a map of name mappings using a list of key:value proto messages of existing name to desired output name.

| Fields       |                                                                                                                                                                                                                         |
|--------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name_map[]` | [`ObjectNameMapping`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.ObjectNameMapping) The elements of the object name map. |

## OracleDialect

This type has no fields.

The dialect definition for Oracle.

## Point

A single data point in a time series.

| Fields     |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
|------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `interval` | [`TimeInterval`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.TimeInterval) The time interval to which the data point applies. For `GAUGE` metrics, the start time does not need to be supplied, but if it is supplied, it must equal the end time. For `DELTA` metrics, the start and end time should specify a non-zero interval, with subsequent points specifying contiguous and non-overlapping intervals. For `CUMULATIVE` metrics, the start and end time should specify a non-zero interval, with subsequent points specifying the same start time and increasing end times, until an event resets the cumulative value to zero and sets a new start time for the following points. |
| `value`    | [`TypedValue`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.TypedValue) The value of the data point.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |

## PostgresqlDialect

This type has no fields.

The dialect definition for Postgresql.

## PrestoDialect

This type has no fields.

The dialect definition for Presto.

## RedshiftDialect

This type has no fields.

The dialect definition for Redshift.

## ResourceErrorDetail

Provides details for errors and the corresponding resources.

| Fields            |                                                                                                                                                                                                                      |
|-------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `resource_info`   | [`ResourceInfo`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.rpc#google.rpc.ResourceInfo) Required. Information about the resource where the error is located.                        |
| `error_details[]` | [`ErrorDetail`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.ErrorDetail) Required. The error details for the resource. |
| `error_count`     | `int32` Required. How many errors there are in total for the resource. Truncation can be indicated by having an `error_count` that is higher than the size of `error_details` .                                      |

## SQLServerDialect

This type has no fields.

The dialect definition for SQL Server.

## SQLiteDialect

This type has no fields.

The dialect definition for SQLite.

## SnowflakeDialect

This type has no fields.

The dialect definition for Snowflake.

## SourceEnv

Represents the default source environment values for the translation.

| Fields                   |                                                                                                                                                                                                                                                                                                                                                                                                          |
|--------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `default_database`       | `string` The default database name to fully qualify SQL objects when their database name is missing.                                                                                                                                                                                                                                                                                                     |
| `schema_search_path[]`   | `string` The schema search path. When SQL objects are missing schema name, translation engine will search through this list to find the value.                                                                                                                                                                                                                                                           |
| `metadata_store_dataset` | `string` Optional. Expects a valid BigQuery dataset ID that exists, e.g., project-123.metadata_store_123. If specified, translation will search and read the required schema information from a metadata store in this dataset. If metadata store doesn't exist, translation will parse the metadata file and upload the schema info to a temp table in the dataset to speed up future translation jobs. |

## SourceEnvironment

Represents the default source environment values for the translation.

| Fields                   |                                                                                                                                                                                                                                                                                                                                                                                                           |
|--------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `default_database`       | `string` The default database name to fully qualify SQL objects when their database name is missing.                                                                                                                                                                                                                                                                                                      |
| `schema_search_path[]`   | `string` The schema search path. When SQL objects are missing schema name, translation engine will search through this list to find the value.                                                                                                                                                                                                                                                            |
| `metadata_store_dataset` | `string` Optional. Expects a validQ BigQuery dataset ID that exists, e.g., project-123.metadata_store_123. If specified, translation will search and read the required schema information from a metadata store in this dataset. If metadata store doesn't exist, translation will parse the metadata file and upload the schema info to a temp table in the dataset to speed up future translation jobs. |

## SourceSpec

Represents one path to the location that holds source data.

| Fields                                                                                     |                                                                                                                                                                                |
|--------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `encoding`                                                                                 | `string` Optional. The optional field to specify the encoding of the sql bytes.                                                                                                |
| Union field `source` . The specific source SQL. `source` can be only one of the following: |                                                                                                                                                                                |
| `base_uri`                                                                                 | `string` The base URI for all files to be read in as sources for translation.                                                                                                  |
| `literal`                                                                                  | [`Literal`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.Literal) Source literal. |
| `gcs_file_path`                                                                            | `string` The path to a single source file in Cloud Storage.                                                                                                                    |

## SourceTargetMapping

Represents one mapping from a source SQL to a target SQL.

| Fields        |                                                                                                                                                                                                         |
|---------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `source_spec` | [`SourceSpec`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.SourceSpec) The source SQL or the path to it.  |
| `target_spec` | [`TargetSpec`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.TargetSpec) The target SQL or the path for it. |

## SparkSQLDialect

This type has no fields.

The dialect definition for SparkSQL.

## StartMigrationWorkflowRequest

A request to start a previously created migration workflow.

| Fields |                                                                                                                          |
|--------|--------------------------------------------------------------------------------------------------------------------------|
| `name` | `string` Required. The unique identifier for the migration workflow. Example: `projects/123/locations/us/workflows/1234` |

## SuggestionConfig

The configuration for the suggestion if requested as a target type.

| Fields                    |                                                                                                                                                                                                                    |
|---------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `skip_suggestion_steps[]` | [`SuggestionStep`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.SuggestionStep) The list of suggestion steps to skip. |

## SuggestionStep

Suggestion step to skip.

| Fields            |                                                                                                                                                                                                                     |
|-------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `suggestion_type` | [`SuggestionType`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.SuggestionStep.SuggestionType) The type of suggestion. |
| `rewrite_target`  | [`RewriteTarget`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.SuggestionStep.RewriteTarget) The rewrite target.       |

## RewriteTarget

The target to apply the suggestion to.

| Enums                        |                             |
|------------------------------|-----------------------------|
| `REWRITE_TARGET_UNSPECIFIED` | Rewrite target unspecified. |
| `SOURCE_SQL`                 | Source SQL.                 |
| `TARGET_SQL`                 | Target SQL.                 |

## SuggestionType

Suggestion type.

| Enums                         |                              |
|-------------------------------|------------------------------|
| `SUGGESTION_TYPE_UNSPECIFIED` | Suggestion type unspecified. |
| `QUERY_CUSTOMIZATION`         | Query customization.         |
| `TRANSLATION_EXPLANATION`     | Translation explanation.     |

## TargetSpec

Represents one path to the location that holds target data.

| Fields          |                                                                                                                                                              |
|-----------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `relative_path` | `string` The relative path for the target data. Given source file `base_uri/input/sql` , the output would be `target_base_uri/sql/relative_path/input.sql` . |

## TaskOutput

The task output for a task type including the status and any errors.

| Fields                                                                                             |                                                                                                                                                                                                                               |
|----------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `state`                                                                                            | [`State`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.TaskOutput.State) Output only. The current state of the task output.      |
| `processing_error`                                                                                 | [`ErrorInfo`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.rpc#google.rpc.ErrorInfo) An explanation that may be populated when the task output is in FAILED state.                              |
| Union field `output` . The detailed output of the task. `output` can be only one of the following: |                                                                                                                                                                                                                               |
| `lineage_output`                                                                                   | [`LineageOutput`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.LineageOutput) The output of the task with output type "LINEAGE". |

## State

Possible task output states.

| Enums               |                                                                                                                                                   |
|---------------------|---------------------------------------------------------------------------------------------------------------------------------------------------|
| `STATE_UNSPECIFIED` | Task output state is unspecified.                                                                                                                 |
| `PENDING`           | Task output is pending.                                                                                                                           |
| `SUCCEEDED`         | Task output is succeeded.                                                                                                                         |
| `FAILED`            | Task output is failed. This does not mean that there is no useful information in the output; partial outputs or failure details may be available. |

## TeradataDialect

The dialect definition for Teradata.

| Fields |                                                                                                                                                                                                                              |
|--------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `mode` | [`Mode`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.TeradataDialect.Mode) Which Teradata sub-dialect mode the user specifies. |

## Mode

The sub-dialect options for Teradata.

| Enums              |                                 |
|--------------------|---------------------------------|
| `MODE_UNSPECIFIED` | Unspecified mode.               |
| `SQL`              | Teradata SQL mode.              |
| `BTEQ`             | BTEQ mode (which includes SQL). |

## TimeInterval

A time interval extending just after a start time through an end time. If the start time is the same as the end time, then the interval represents a single point in time.

| Fields       |                                                                                                                                                                                                                                           |
|--------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `start_time` | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) Optional. The beginning of the time interval. The default value for the start time is the end time. The start time must not be later than the end time. |
| `end_time`   | [`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp) Required. The end of the time interval.                                                                                                                 |

## TimeSeries

The metrics object for a SubTask.

| Fields        |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
|---------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `metric`      | `string` Required. The name of the metric. If the metric is not known by the service yet, it will be auto-created.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| `value_type`  | [`ValueType`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.api#google.api.MetricDescriptor.ValueType) Required. The value type of the time series.                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| `metric_kind` | [`MetricKind`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.api#google.api.MetricDescriptor.MetricKind) Optional. The metric kind of the time series. If present, it must be the same as the metric kind of the associated metric. If the associated metric's descriptor must be auto-created, then this field specifies the metric kind of the new descriptor and must be either `GAUGE` (the default) or `CUMULATIVE` .                                                                                                                                                                                      |
| `points[]`    | [`Point`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.Point) Required. The data points of this time series. When listing time series, points are returned in reverse time order. When creating a time series, this field must contain exactly one point and the point's type must be the same as the value type of the associated metric. If the associated metric's descriptor must be auto-created, then the value type of the descriptor is determined by the point's type, which must be `BOOL` , `INT64` , `DOUBLE` , or `DISTRIBUTION` . |

## TranslationConfigDetails

The translation config to capture necessary settings for a translation task and subtask.

| Fields                                                                                                                                                                           |                                                                                                                                                                                                                                                               |
|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `source_dialect`                                                                                                                                                                 | [`Dialect`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.Dialect) The dialect of the input files.                                                                |
| `target_dialect`                                                                                                                                                                 | [`Dialect`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.Dialect) The target dialect for the engine to translate the input to.                                   |
| `source_env`                                                                                                                                                                     | [`SourceEnv`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.SourceEnv) The default source environment values for the translation.                                 |
| `request_source`                                                                                                                                                                 | `string` The indicator to show translation request initiator.                                                                                                                                                                                                 |
| `target_types[]`                                                                                                                                                                 | `string` The types of output to generate, e.g. sql, metadata etc. If not specified, a default set of targets will be generated. Some additional target types may be slower to generate. See the documentation for the set of available target types.          |
| Union field `source_location` . The chosen path where the source for input files will be found. `source_location` can be only one of the following:                              |                                                                                                                                                                                                                                                               |
| `gcs_source_path`                                                                                                                                                                | `string` The Cloud Storage path for a directory of files to translate in a task.                                                                                                                                                                              |
| Union field `target_location` . The chosen path where the destination for output files will be found. `target_location` can be only one of the following:                        |                                                                                                                                                                                                                                                               |
| `gcs_target_path`                                                                                                                                                                | `string` The Cloud Storage path to write back the corresponding input files to.                                                                                                                                                                               |
| Union field `output_name_mapping` . The mapping of full SQL object names from their current state to the desired output. `output_name_mapping` can be only one of the following: |                                                                                                                                                                                                                                                               |
| `name_mapping_list`                                                                                                                                                              | [`ObjectNameMappingList`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.ObjectNameMappingList) The mapping of objects to their desired output names in list form. |

## TranslationDetails

The translation details to capture the necessary settings for a translation job.

| Fields                     |                                                                                                                                                                                                                                                                                 |
|----------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `source_target_mapping[]`  | [`SourceTargetMapping`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.SourceTargetMapping) The mapping from source to target SQL.                                                   |
| `target_base_uri`          | `string` The base URI for all writes to persistent storage.                                                                                                                                                                                                                     |
| `source_environment`       | [`SourceEnvironment`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.SourceEnvironment) The default source environment values for the translation.                                   |
| `target_return_literals[]` | `string` The list of literal targets that will be directly returned to the response. Each entry consists of the constructed path, EXCLUDING the base path. Not providing a target_base_uri will prevent writing to persistent storage.                                          |
| `target_types[]`           | `string` The types of output to generate, e.g. sql, metadata, lineage_from_sql_scripts, etc. If not specified, a default set of targets will be generated. Some additional target types may be slower to generate. See the documentation for the set of available target types. |
| `suggestion_config`        | [`SuggestionConfig`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.SuggestionConfig) The configuration for the suggestion if requested as a target type.                            |

## TranslationTaskResult

Translation specific result details from the migration task.

| Fields                  |                                                                                                                                                                                                                                                            |
|-------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `translated_literals[]` | [`Literal`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.Literal) The list of the translated literals.                                                        |
| `report_log_messages[]` | [`GcsReportLogMessage`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.cloud.bigquery.migration.v2#google.cloud.bigquery.migration.v2.GcsReportLogMessage) The records from the aggregate CSV report for a migration workflow. |
| `console_uri`           | `string` The Cloud Console URI for the migration workflow.                                                                                                                                                                                                 |

## TypedValue

A single strongly-typed value.

| Fields                                                                                 |                                                                                                                                                          |
|----------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `value` . The typed value field. `value` can be only one of the following: |                                                                                                                                                          |
| `bool_value`                                                                           | `bool` A Boolean value: `true` or `false` .                                                                                                              |
| `int64_value`                                                                          | `int64` A 64-bit integer. Its range is approximately `+/-9.2x10^18` .                                                                                    |
| `double_value`                                                                         | `double` A 64-bit double-precision floating-point number. Its magnitude is approximately `+/-10^(+/-300)` and it has 16 significant digits of precision. |
| `string_value`                                                                         | `string` A variable-length string value.                                                                                                                 |
| `distribution_value`                                                                   | [`Distribution`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rpc/google.api#google.api.Distribution) A distribution value.           |

## VerticaDialect

This type has no fields.

The dialect definition for Vertica.
