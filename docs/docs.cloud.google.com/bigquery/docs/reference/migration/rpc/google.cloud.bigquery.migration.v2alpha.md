## Index

  - `  MigrationService  ` (interface)
  - `  AssessmentFeatureHandle  ` (message)
  - `  AssessmentOrchestrationResultDetails  ` (message)
  - `  AssessmentTaskDetails  ` (message)
  - `  AzureSynapseDialect  ` (message)
  - `  BigQueryDialect  ` (message)
  - `  BteqOptions  ` (message)
  - `  CreateMigrationWorkflowRequest  ` (message)
  - `  DB2Dialect  ` (message)
  - `  DatasetReference  ` (message)
  - `  DeleteMigrationWorkflowRequest  ` (message)
  - `  Dialect  ` (message)
  - `  ErrorDetail  ` (message)
  - `  ErrorLocation  ` (message)
  - `  Filter  ` (message)
  - `  GcsReportLogMessage  ` (message)
  - `  GetMigrationSubtaskRequest  ` (message)
  - `  GetMigrationWorkflowRequest  ` (message)
  - `  GreenplumDialect  ` (message)
  - `  HiveQLDialect  ` (message)
  - `  IdentifierSettings  ` (message)
  - `  IdentifierSettings.IdentifierCase  ` (enum)
  - `  IdentifierSettings.IdentifierRewriteMode  ` (enum)
  - `  ListMigrationSubtasksRequest  ` (message)
  - `  ListMigrationSubtasksResponse  ` (message)
  - `  ListMigrationWorkflowsRequest  ` (message)
  - `  ListMigrationWorkflowsResponse  ` (message)
  - `  Literal  ` (message)
  - `  MetadataCaching  ` (message)
  - `  MigrationSubtask  ` (message)
  - `  MigrationSubtask.State  ` (enum)
  - `  MigrationTask  ` (message)
  - `  MigrationTask.State  ` (enum)
  - `  MigrationTaskOrchestrationResult  ` (message)
  - `  MigrationTaskResult  ` (message)
  - `  MigrationWorkflow  ` (message)
  - `  MigrationWorkflow.State  ` (enum)
  - `  MySQLDialect  ` (message)
  - `  NameMappingKey  ` (message)
  - `  NameMappingKey.Type  ` (enum)
  - `  NameMappingValue  ` (message)
  - `  NetezzaDialect  ` (message)
  - `  ObjectNameMapping  ` (message)
  - `  ObjectNameMappingList  ` (message)
  - `  OracleDialect  ` (message)
  - `  Point  ` (message)
  - `  PostgresqlDialect  ` (message)
  - `  PrestoDialect  ` (message)
  - `  RedshiftDialect  ` (message)
  - `  ResourceErrorDetail  ` (message)
  - `  SQLServerDialect  ` (message)
  - `  SQLiteDialect  ` (message)
  - `  SnowflakeDialect  ` (message)
  - `  SourceEnv  ` (message)
  - `  SourceEnvironment  ` (message)
  - `  SourceLocation  ` (message)
  - `  SourceSpec  ` (message)
  - `  SourceTargetLocationMapping  ` (message)
  - `  SourceTargetMapping  ` (message)
  - `  SparkSQLDialect  ` (message)
  - `  StartMigrationWorkflowRequest  ` (message)
  - `  TargetLocation  ` (message)
  - `  TargetSpec  ` (message)
  - `  TeradataDialect  ` (message)
  - `  TeradataDialect.Mode  ` (enum)
  - `  TeradataOptions  ` (message)
  - `  TimeInterval  ` (message)
  - `  TimeSeries  ` (message)
  - `  TranslationConfigDetails  ` (message)
  - `  TranslationDetails  ` (message)
  - `  TranslationFileMapping  ` (message)
  - `  TranslationTaskDetails  ` (message)
  - `  TranslationTaskDetails.FileEncoding  ` (enum)
  - `  TranslationTaskDetails.TokenType  ` (enum)
  - `  TranslationTaskResult  ` (message)
  - `  TypedValue  ` (message)
  - `  VerticaDialect  ` (message)

## MigrationService

Service to handle EDW migrations.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>CreateMigrationWorkflow</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">           rpc CreateMigrationWorkflow(                         CreateMigrationWorkflowRequest            </code> ) returns ( <code dir="ltr" translate="no">              MigrationWorkflow            </code> )</p>
<p>Creates a migration workflow.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/cloud-platform             </code></li>
</ul>
<p>For more information, see the <a href="/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl>
<dl>
<dt>IAM Permissions</dt>
<dd><p>Requires the following <a href="https://cloud.google.com/iam/docs">IAM</a> permission on the <code dir="ltr" translate="no">             parent            </code> resource:</p>
<ul>
<li><code dir="ltr" translate="no">              bigquerymigration.workflows.create             </code></li>
</ul>
<p>For more information, see the <a href="https://cloud.google.com/iam/docs">IAM documentation</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>DeleteMigrationWorkflow</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">           rpc DeleteMigrationWorkflow(                         DeleteMigrationWorkflowRequest            </code> ) returns ( <code dir="ltr" translate="no">              Empty            </code> )</p>
<p>Deletes a migration workflow by name.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/cloud-platform             </code></li>
</ul>
<p>For more information, see the <a href="/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl>
<dl>
<dt>IAM Permissions</dt>
<dd><p>Requires the following <a href="https://cloud.google.com/iam/docs">IAM</a> permission on the <code dir="ltr" translate="no">             name            </code> resource:</p>
<ul>
<li><code dir="ltr" translate="no">              bigquerymigration.workflows.delete             </code></li>
</ul>
<p>For more information, see the <a href="https://cloud.google.com/iam/docs">IAM documentation</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>GetMigrationSubtask</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">           rpc GetMigrationSubtask(                         GetMigrationSubtaskRequest            </code> ) returns ( <code dir="ltr" translate="no">              MigrationSubtask            </code> )</p>
<p>Gets a previously created migration subtask.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/cloud-platform             </code></li>
</ul>
<p>For more information, see the <a href="/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl>
<dl>
<dt>IAM Permissions</dt>
<dd><p>Requires the following <a href="https://cloud.google.com/iam/docs">IAM</a> permission on the <code dir="ltr" translate="no">             name            </code> resource:</p>
<ul>
<li><code dir="ltr" translate="no">              bigquerymigration.subtasks.get             </code></li>
</ul>
<p>For more information, see the <a href="https://cloud.google.com/iam/docs">IAM documentation</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>GetMigrationWorkflow</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">           rpc GetMigrationWorkflow(                         GetMigrationWorkflowRequest            </code> ) returns ( <code dir="ltr" translate="no">              MigrationWorkflow            </code> )</p>
<p>Gets a previously created migration workflow.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/cloud-platform             </code></li>
</ul>
<p>For more information, see the <a href="/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl>
<dl>
<dt>IAM Permissions</dt>
<dd><p>Requires the following <a href="https://cloud.google.com/iam/docs">IAM</a> permission on the <code dir="ltr" translate="no">             name            </code> resource:</p>
<ul>
<li><code dir="ltr" translate="no">              bigquerymigration.workflows.get             </code></li>
</ul>
<p>For more information, see the <a href="https://cloud.google.com/iam/docs">IAM documentation</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>ListMigrationSubtasks</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">           rpc ListMigrationSubtasks(                         ListMigrationSubtasksRequest            </code> ) returns ( <code dir="ltr" translate="no">              ListMigrationSubtasksResponse            </code> )</p>
<p>Lists previously created migration subtasks.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/cloud-platform             </code></li>
</ul>
<p>For more information, see the <a href="/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl>
<dl>
<dt>IAM Permissions</dt>
<dd><p>Requires the following <a href="https://cloud.google.com/iam/docs">IAM</a> permission on the <code dir="ltr" translate="no">             parent            </code> resource:</p>
<ul>
<li><code dir="ltr" translate="no">              bigquerymigration.subtasks.list             </code></li>
</ul>
<p>For more information, see the <a href="https://cloud.google.com/iam/docs">IAM documentation</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>ListMigrationWorkflows</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">           rpc ListMigrationWorkflows(                         ListMigrationWorkflowsRequest            </code> ) returns ( <code dir="ltr" translate="no">              ListMigrationWorkflowsResponse            </code> )</p>
<p>Lists previously created migration workflow.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/cloud-platform             </code></li>
</ul>
<p>For more information, see the <a href="/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl>
<dl>
<dt>IAM Permissions</dt>
<dd><p>Requires the following <a href="https://cloud.google.com/iam/docs">IAM</a> permission on the <code dir="ltr" translate="no">             parent            </code> resource:</p>
<ul>
<li><code dir="ltr" translate="no">              bigquerymigration.workflows.list             </code></li>
</ul>
<p>For more information, see the <a href="https://cloud.google.com/iam/docs">IAM documentation</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>StartMigrationWorkflow</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">           rpc StartMigrationWorkflow(                         StartMigrationWorkflowRequest            </code> ) returns ( <code dir="ltr" translate="no">              Empty            </code> )</p>
<p>Starts a previously created migration workflow. I.e., the state transitions from DRAFT to RUNNING. This is a no-op if the state is already RUNNING. An error will be signaled if the state is anything other than DRAFT or RUNNING.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/cloud-platform             </code></li>
</ul>
<p>For more information, see the <a href="/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl>
<dl>
<dt>IAM Permissions</dt>
<dd><p>Requires the following <a href="https://cloud.google.com/iam/docs">IAM</a> permission on the <code dir="ltr" translate="no">             name            </code> resource:</p>
<ul>
<li><code dir="ltr" translate="no">              bigquerymigration.workflows.update             </code></li>
</ul>
<p>For more information, see the <a href="https://cloud.google.com/iam/docs">IAM documentation</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

## AssessmentFeatureHandle

User-definable feature flags for assessment tasks.

Fields

`  add_shareable_dataset  `

`  bool  `

Optional. Whether to create a dataset containing non-PII data in addition to the output dataset.

## AssessmentOrchestrationResultDetails

Details for an assessment task orchestration result.

Fields

`  output_tables_schema_version  `

`  string  `

Optional. The version used for the output table schemas.

`  report_uri  `

`  string  `

Optional. The URI of the Data Studio report.

`  additional_report_uris  `

`  map<string, string>  `

Optional. Mapping with additional report URIs. This gives a mapping of report names to their URIs. The possible values for the keys are documented in the user guide.

## AssessmentTaskDetails

Assessment task config.

Fields

`  input_path  `

`  string  `

Required. The Cloud Storage path for assessment input files.

`  output_dataset  `

`  string  `

Required. The BigQuery dataset for output.

`  querylogs_path  `

`  string  `

Optional. An optional Cloud Storage path to write the query logs (which is then used as an input path on the translation task)

`  data_source  `

`  string  `

Required. The data source or data warehouse type (eg: TERADATA/REDSHIFT) from which the input data is extracted.

`  feature_handle  `

`  AssessmentFeatureHandle  `

Optional. A collection of additional feature flags for this assessment.

## AzureSynapseDialect

This type has no fields.

The dialect definition for Azure Synapse.

## BigQueryDialect

This type has no fields.

The dialect definition for BigQuery.

## BteqOptions

BTEQ translation task related settings.

Fields

`  project_dataset  `

`  DatasetReference  `

Specifies the project and dataset in BigQuery that will be used for external table creation during the translation.

`  default_path_uri  `

`  string  `

The Cloud Storage location to be used as the default path for files that are not otherwise specified in the file replacement map.

`  file_replacement_map  `

`  map<string, string>  `

Maps the local paths that are used in BTEQ scripts (the keys) to the paths in Cloud Storage that should be used in their stead in the translation (the value).

## CreateMigrationWorkflowRequest

Request to create a migration workflow resource.

Fields

`  parent  `

`  string  `

Required. The name of the project to which this migration workflow belongs. Example: `  projects/foo/locations/bar  `

`  migration_workflow  `

`  MigrationWorkflow  `

Required. The migration workflow to create.

## DB2Dialect

This type has no fields.

The dialect definition for DB2.

## DatasetReference

Reference to a BigQuery dataset.

Fields

`  dataset_id  `

`  string  `

A unique ID for this dataset, without the project name. The ID must contain only letters (a-z, A-Z), numbers (0-9), or underscores (\_). The maximum length is 1,024 characters.

`  project_id  `

`  string  `

The ID of the project containing this dataset.

`  dataset_id_alternative[]  `

`  string  `

The alternative field that will be used when the service is not able to translate the received data to the dataset\_id field.

`  project_id_alternative[]  `

`  string  `

The alternative field that will be used when the service is not able to translate the received data to the project\_id field.

## DeleteMigrationWorkflowRequest

A request to delete a previously created migration workflow.

Fields

`  name  `

`  string  `

Required. The unique identifier for the migration workflow. Example: `  projects/123/locations/us/workflows/1234  `

## Dialect

The possible dialect options for translation.

Fields

Union field `  dialect_value  ` . The possible dialect options that this message represents. `  dialect_value  ` can be only one of the following:

`  bigquery_dialect  `

`  BigQueryDialect  `

The BigQuery dialect

`  hiveql_dialect  `

`  HiveQLDialect  `

The HiveQL dialect

`  redshift_dialect  `

`  RedshiftDialect  `

The Redshift dialect

`  teradata_dialect  `

`  TeradataDialect  `

The Teradata dialect

`  oracle_dialect  `

`  OracleDialect  `

The Oracle dialect

`  sparksql_dialect  `

`  SparkSQLDialect  `

The SparkSQL dialect

`  snowflake_dialect  `

`  SnowflakeDialect  `

The Snowflake dialect

`  netezza_dialect  `

`  NetezzaDialect  `

The Netezza dialect

`  azure_synapse_dialect  `

`  AzureSynapseDialect  `

The Azure Synapse dialect

`  vertica_dialect  `

`  VerticaDialect  `

The Vertica dialect

`  sql_server_dialect  `

`  SQLServerDialect  `

The SQL Server dialect

`  postgresql_dialect  `

`  PostgresqlDialect  `

The Postgresql dialect

`  presto_dialect  `

`  PrestoDialect  `

The Presto dialect

`  mysql_dialect  `

`  MySQLDialect  `

The MySQL dialect

`  db2_dialect  `

`  DB2Dialect  `

DB2 dialect

`  sqlite_dialect  `

`  SQLiteDialect  `

SQLite dialect

`  greenplum_dialect  `

`  GreenplumDialect  `

Greenplum dialect

## ErrorDetail

Provides details for errors, e.g. issues that where encountered when processing a subtask.

Fields

`  location  `

`  ErrorLocation  `

Optional. The exact location within the resource (if applicable).

`  error_info  `

`  ErrorInfo  `

Required. Describes the cause of the error with structured detail.

## ErrorLocation

Holds information about where the error is located.

Fields

`  line  `

`  int32  `

Optional. If applicable, denotes the line where the error occurred. A zero value means that there is no line information.

`  column  `

`  int32  `

Optional. If applicable, denotes the column where the error occurred. A zero value means that there is no columns information.

## Filter

The filter applied to fields of translation details.

Fields

`  input_file_exclusion_prefixes[]  `

`  string  `

The list of prefixes used to exclude processing for input files.

## GcsReportLogMessage

A record in the aggregate CSV report for a migration workflow

Fields

`  severity  `

`  string  `

Severity of the translation record.

`  category  `

`  string  `

Category of the error/warning. Example: SyntaxError

`  file_path  `

`  string  `

The file path in which the error occurred

`  filename  `

`  string  `

The file name in which the error occurred

`  source_script_line  `

`  int32  `

Specifies the row from the source text where the error occurred (0 based, -1 for messages without line location). Example: 2

`  source_script_column  `

`  int32  `

Specifies the column from the source texts where the error occurred. (0 based, -1 for messages without column location) example: 6

`  message  `

`  string  `

Detailed message of the record.

`  script_context  `

`  string  `

The script context (obfuscated) in which the error occurred

`  action  `

`  string  `

Category of the error/warning. Example: SyntaxError

`  effect  `

`  string  `

Effect of the error/warning. Example: COMPATIBILITY

`  object_name  `

`  string  `

Name of the affected object in the log message.

## GetMigrationSubtaskRequest

A request to get a previously created migration subtasks.

Fields

`  name  `

`  string  `

Required. The unique identifier for the migration subtask. Example: `  projects/123/locations/us/workflows/1234/subtasks/543  `

`  read_mask  `

`  FieldMask  `

Optional. The list of fields to be retrieved.

## GetMigrationWorkflowRequest

A request to get a previously created migration workflow.

Fields

`  name  `

`  string  `

Required. The unique identifier for the migration workflow. Example: `  projects/123/locations/us/workflows/1234  `

`  read_mask  `

`  FieldMask  `

The list of fields to be retrieved.

## GreenplumDialect

This type has no fields.

The dialect definition for Greenplum.

## HiveQLDialect

This type has no fields.

The dialect definition for HiveQL.

## IdentifierSettings

Settings related to SQL identifiers.

Fields

`  output_identifier_case  `

`  IdentifierCase  `

The setting to control output queries' identifier case.

`  identifier_rewrite_mode  `

`  IdentifierRewriteMode  `

Specifies the rewrite mode for SQL identifiers.

## IdentifierCase

The identifier case type.

Enums

`  IDENTIFIER_CASE_UNSPECIFIED  `

The identifier case is not specified.

`  ORIGINAL  `

Identifiers' cases will be kept as the original cases.

`  UPPER  `

Identifiers will be in upper cases.

`  LOWER  `

Identifiers will be in lower cases.

## IdentifierRewriteMode

The SQL identifier rewrite mode.

Enums

`  IDENTIFIER_REWRITE_MODE_UNSPECIFIED  `

SQL Identifier rewrite mode is unspecified.

`  NONE  `

SQL identifiers won't be rewrite.

`  REWRITE_ALL  `

All SQL identifiers will be rewrite.

## ListMigrationSubtasksRequest

A request to list previously created migration subtasks.

Fields

`  parent  `

`  string  `

Required. The migration task of the subtasks to list. Example: `  projects/123/locations/us/workflows/1234  `

`  read_mask  `

`  FieldMask  `

Optional. The list of fields to be retrieved.

`  page_size  `

`  int32  `

Optional. The maximum number of migration tasks to return. The service may return fewer than this number.

`  page_token  `

`  string  `

Optional. A page token, received from previous `  ListMigrationSubtasks  ` call. Provide this to retrieve the subsequent page.

When paginating, all other parameters provided to `  ListMigrationSubtasks  ` must match the call that provided the page token.

`  filter  `

`  string  `

Optional. The filter to apply. This can be used to get the subtasks of a specific tasks in a workflow, e.g. `  migration_task = "ab012"  ` where `  "ab012"  ` is the task ID (not the name in the named map).

## ListMigrationSubtasksResponse

Response object for a `  ListMigrationSubtasks  ` call.

Fields

`  migration_subtasks[]  `

`  MigrationSubtask  `

The migration subtasks for the specified task.

`  next_page_token  `

`  string  `

A token, which can be sent as `  page_token  ` to retrieve the next page. If this field is omitted, there are no subsequent pages.

## ListMigrationWorkflowsRequest

A request to list previously created migration workflows.

Fields

`  parent  `

`  string  `

Required. The project and location of the migration workflows to list. Example: `  projects/123/locations/us  `

`  read_mask  `

`  FieldMask  `

The list of fields to be retrieved.

`  page_size  `

`  int32  `

The maximum number of migration workflows to return. The service may return fewer than this number.

`  page_token  `

`  string  `

A page token, received from previous `  ListMigrationWorkflows  ` call. Provide this to retrieve the subsequent page.

When paginating, all other parameters provided to `  ListMigrationWorkflows  ` must match the call that provided the page token.

`  filter  `

`  string  `

Optional. An optional AIP-160 filter to apply. The following attributes are supported: `  display_name  ` , `  state  ` , `  task.name  ` , and `  task.type  ` .

`  order_by  `

`  string  `

Optional. An optional AIP-132 order by field. The following attributes are supported: `  display_name  ` , `  state  ` , `  task.name  ` , and `  task.type  ` .

## ListMigrationWorkflowsResponse

Response object for a `  ListMigrationWorkflows  ` call.

Fields

`  migration_workflows[]  `

`  MigrationWorkflow  `

The migration workflows for the specified project / location.

`  next_page_token  `

`  string  `

A token, which can be sent as `  page_token  ` to retrieve the next page. If this field is omitted, there are no subsequent pages.

## Literal

Literal data.

Fields

`  relative_path  `

`  string  `

Required. The identifier of the literal entry.

Union field `  literal_data  ` . The literal SQL contents. `  literal_data  ` can be only one of the following:

`  literal_string  `

`  string  `

Literal string data.

`  literal_bytes  `

`  bytes  `

Literal byte data.

## MetadataCaching

Metadata caching settings.

Fields

`  max_cache_age  `

`  Duration  `

Optional. The maximum age of the metadata cache. If the cache is older than this value, the cache will be refreshed. A cache will not be kept for longer than 7 days. Providing no value or a value larger than 7 days will result in using the cache if available (i.e. the same as setting the value to 7 days).

Setting the duration to 0 or a negative value will refresh the cache.

## MigrationSubtask

A subtask for a migration which carries details about the configuration of the subtask. The content of the details should not matter to the end user, but is a contract between the subtask creator and subtask worker.

Fields

`  name  `

`  string  `

Output only. Immutable. The resource name for the migration subtask. The ID is server-generated.

Example: `  projects/123/locations/us/workflows/345/subtasks/678  `

`  task_id  `

`  string  `

The unique ID of the task to which this subtask belongs.

`  type  `

`  string  `

The type of the Subtask. The migration service does not check whether this is a known type. It is up to the task creator (i.e. orchestrator or worker) to ensure it only creates subtasks for which there are compatible workers polling for Subtasks.

`  state  `

`  State  `

Output only. The current state of the subtask.

`  processing_error  `

`  ErrorInfo  `

Output only. An explanation that may be populated when the task is in FAILED state.

`  resource_error_details[]  `

`  ResourceErrorDetail  `

Output only. Provides details to errors and issues encountered while processing the subtask. Presence of error details does not mean that the subtask failed.

`  resource_error_count  `

`  int32  `

Output only. The number or resources with errors. Note: This is not the total number of errors as each resource can have more than one error. This is used to indicate truncation by having a `  resource_error_count  ` that is higher than the size of `  resource_error_details  ` .

`  create_time  `

`  Timestamp  `

Output only. Time when the subtask was created.

`  last_update_time  `

`  Timestamp  `

Output only. Time when the subtask was last updated.

`  metrics[]  `

`  TimeSeries  `

Output only. The metrics for the subtask.

## State

Possible states of a migration subtask.

Enums

`  STATE_UNSPECIFIED  `

The state is unspecified.

`  ACTIVE  `

The subtask is ready, i.e. it is ready for execution.

`  RUNNING  `

The subtask is running, i.e. it is assigned to a worker for execution.

`  SUCCEEDED  `

The subtask finished successfully.

`  FAILED  `

The subtask finished unsuccessfully.

`  PAUSED  `

The subtask is paused, i.e., it will not be scheduled. If it was already assigned,it might still finish but no new lease renewals will be granted.

`  PENDING_DEPENDENCY  `

The subtask is pending a dependency. It will be scheduled once its dependencies are done.

## MigrationTask

A single task for a migration which has details about the configuration of the task.

Fields

`  id  `

`  string  `

Output only. Immutable. The unique identifier for the migration task. The ID is server-generated.

`  type  `

`  string  `

The type of the task. This must be one of the supported task types: Translation\_Teradata2BQ, Translation\_Redshift2BQ, Translation\_Bteq2BQ, Translation\_Oracle2BQ, Translation\_HiveQL2BQ, Translation\_SparkSQL2BQ, Translation\_Snowflake2BQ, Translation\_Netezza2BQ, Translation\_AzureSynapse2BQ, Translation\_Vertica2BQ, Translation\_SQLServer2BQ, Translation\_Presto2BQ, Translation\_MySQL2BQ, Translation\_Postgresql2BQ, Translation\_SQLite2BQ, Translation\_Greenplum2BQ.

`  details  `

`  Any  `

DEPRECATED\! Use one of the task\_details below. The details of the task. The type URL must be one of the supported task details messages and correspond to the Task's type.

`  state  `

`  State  `

Output only. The current state of the task.

`  processing_error  `

`  ErrorInfo  `

Output only. An explanation that may be populated when the task is in FAILED state.

`  create_time  `

`  Timestamp  `

Output only. Time when the task was created.

`  last_update_time  `

`  Timestamp  `

Output only. Time when the task was last updated.

`  orchestration_result (deprecated)  `

`  MigrationTaskOrchestrationResult  `

This item is deprecated\!

Output only. Deprecated: Use the task\_result field below instead. Additional information about the orchestration.

`  resource_error_details[]  `

`  ResourceErrorDetail  `

Output only. Provides details to errors and issues encountered while processing the task. Presence of error details does not mean that the task failed.

`  resource_error_count  `

`  int32  `

The number or resources with errors. Note: This is not the total number of errors as each resource can have more than one error. This is used to indicate truncation by having a `  resource_error_count  ` that is higher than the size of `  resource_error_details  ` .

`  metrics[]  `

`  TimeSeries  `

Output only. The metrics for the task.

`  task_result  `

`  MigrationTaskResult  `

Output only. The result of the task.

`  total_processing_error_count  `

`  int32  `

Output only. Count of all the processing errors in this task and its subtasks.

`  total_resource_error_count  `

`  int32  `

Output only. Count of all the resource errors in this task and its subtasks.

Union field `  task_details  ` . The details of the task. `  task_details  ` can be only one of the following:

`  assessment_task_details  `

`  AssessmentTaskDetails  `

Task configuration for Assessment.

`  translation_task_details  `

`  TranslationTaskDetails  `

Task configuration for Batch SQL Translation.

`  translation_config_details  `

`  TranslationConfigDetails  `

Task configuration for CW Batch/Offline SQL Translation.

`  translation_details  `

`  TranslationDetails  `

Task details for unified SQL Translation.

## State

Possible states of a migration task.

Enums

`  STATE_UNSPECIFIED  `

The state is unspecified.

`  PENDING  `

The task is waiting for orchestration.

`  ORCHESTRATING  `

The task is assigned to an orchestrator.

`  RUNNING  `

The task is running, i.e. its subtasks are ready for execution.

`  PAUSED  `

The task is paused. Assigned subtasks can continue, but no new subtasks will be scheduled.

`  SUCCEEDED  `

The task finished successfully.

`  FAILED  `

The task finished unsuccessfully.

## MigrationTaskOrchestrationResult

Additional information from the orchestrator when it is done with the task orchestration.

Fields

Union field `  details  ` . Details specific to the task type. `  details  ` can be only one of the following:

`  assessment_details  `

`  AssessmentOrchestrationResultDetails  `

Details specific to assessment task types.

`  translation_task_result  `

`  TranslationTaskResult  `

Details specific to translation task types.

## MigrationTaskResult

The migration task result.

Fields

Union field `  details  ` . Details specific to the task type. `  details  ` can be only one of the following:

`  assessment_details  `

`  AssessmentOrchestrationResultDetails  `

Details specific to assessment task types.

`  translation_task_result  `

`  TranslationTaskResult  `

Details specific to translation task types.

## MigrationWorkflow

A migration workflow which specifies what needs to be done for an EDW migration.

Fields

`  name  `

`  string  `

Output only. Immutable. Identifier. The unique identifier for the migration workflow. The ID is server-generated.

Example: `  projects/123/locations/us/workflows/345  `

`  display_name  `

`  string  `

The display name of the workflow. This can be set to give a workflow a descriptive name. There is no guarantee or enforcement of uniqueness.

`  tasks  `

`  map<string, MigrationTask  ` \>

The tasks in a workflow in a named map. The name (i.e. key) has no meaning and is merely a convenient way to address a specific task in a workflow.

`  state  `

`  State  `

Output only. That status of the workflow.

`  create_time  `

`  Timestamp  `

Output only. Time when the workflow was created.

`  last_update_time  `

`  Timestamp  `

Output only. Time when the workflow was last updated.

## State

Possible migration workflow states.

Enums

`  STATE_UNSPECIFIED  `

Workflow state is unspecified.

`  DRAFT  `

Workflow is in draft status, i.e. tasks are not yet eligible for execution.

`  RUNNING  `

Workflow is running (i.e. tasks are eligible for execution).

`  PAUSED  `

Workflow is paused. Tasks currently in progress may continue, but no further tasks will be scheduled.

`  COMPLETED  `

Workflow is complete. There should not be any task in a non-terminal state, but if they are (e.g. forced termination), they will not be scheduled.

## MySQLDialect

This type has no fields.

The dialect definition for MySQL.

## NameMappingKey

The potential components of a full name mapping that will be mapped during translation in the source data warehouse.

Fields

`  type  `

`  Type  `

The type of object that is being mapped.

`  database  `

`  string  `

The database name (BigQuery project ID equivalent in the source data warehouse).

`  schema  `

`  string  `

The schema name (BigQuery dataset equivalent in the source data warehouse).

`  relation  `

`  string  `

The relation name (BigQuery table or view equivalent in the source data warehouse).

`  attribute  `

`  string  `

The attribute name (BigQuery column equivalent in the source data warehouse).

## Type

The type of the object that is being mapped.

Enums

`  TYPE_UNSPECIFIED  `

Unspecified name mapping type.

`  DATABASE  `

The object being mapped is a database.

`  SCHEMA  `

The object being mapped is a schema.

`  RELATION  `

The object being mapped is a relation.

`  ATTRIBUTE  `

The object being mapped is an attribute.

`  RELATION_ALIAS  `

The object being mapped is a relation alias.

`  ATTRIBUTE_ALIAS  `

The object being mapped is a an attribute alias.

`  FUNCTION  `

The object being mapped is a function.

## NameMappingValue

The potential components of a full name mapping that will be mapped during translation in the target data warehouse.

Fields

`  database  `

`  string  `

The database name (BigQuery project ID equivalent in the target data warehouse).

`  schema  `

`  string  `

The schema name (BigQuery dataset equivalent in the target data warehouse).

`  relation  `

`  string  `

The relation name (BigQuery table or view equivalent in the target data warehouse).

`  attribute  `

`  string  `

The attribute name (BigQuery column equivalent in the target data warehouse).

## NetezzaDialect

This type has no fields.

The dialect definition for Netezza.

## ObjectNameMapping

Represents a key-value pair of NameMappingKey to NameMappingValue to represent the mapping of SQL names from the input value to desired output.

Fields

`  source  `

`  NameMappingKey  `

The name of the object in source that is being mapped.

`  target  `

`  NameMappingValue  `

The desired target name of the object that is being mapped.

## ObjectNameMappingList

Represents a map of name mappings using a list of key:value proto messages of existing name to desired output name.

Fields

`  name_map[]  `

`  ObjectNameMapping  `

The elements of the object name map.

## OracleDialect

This type has no fields.

The dialect definition for Oracle.

## Point

A single data point in a time series.

Fields

`  interval  `

`  TimeInterval  `

The time interval to which the data point applies. For `  GAUGE  ` metrics, the start time does not need to be supplied, but if it is supplied, it must equal the end time. For `  DELTA  ` metrics, the start and end time should specify a non-zero interval, with subsequent points specifying contiguous and non-overlapping intervals. For `  CUMULATIVE  ` metrics, the start and end time should specify a non-zero interval, with subsequent points specifying the same start time and increasing end times, until an event resets the cumulative value to zero and sets a new start time for the following points.

`  value  `

`  TypedValue  `

The value of the data point.

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

Fields

`  resource_info  `

`  ResourceInfo  `

Required. Information about the resource where the error is located.

`  error_details[]  `

`  ErrorDetail  `

Required. The error details for the resource.

`  error_count  `

`  int32  `

Required. How many errors there are in total for the resource. Truncation can be indicated by having an `  error_count  ` that is higher than the size of `  error_details  ` .

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

Fields

`  default_database  `

`  string  `

The default database name to fully qualify SQL objects when their database name is missing.

`  schema_search_path[]  `

`  string  `

The schema search path. When SQL objects are missing schema name, translation engine will search through this list to find the value.

`  metadata_store_dataset  `

`  string  `

Optional. Expects a valid BigQuery dataset ID that exists, e.g., project-123.metadata\_store\_123. If specified, translation will search and read the required schema information from a metadata store in this dataset. If metadata store doesn't exist, translation will parse the metadata file and upload the schema info to a temp table in the dataset to speed up future translation jobs.

## SourceEnvironment

Represents the default source environment values for the translation.

Fields

`  default_database  `

`  string  `

The default database name to fully qualify SQL objects when their database name is missing.

`  schema_search_path[]  `

`  string  `

The schema search path. When SQL objects are missing schema name, translation engine will search through this list to find the value.

`  metadata_store_dataset  `

`  string  `

Optional. Expects a validQ BigQuery dataset ID that exists, e.g., project-123.metadata\_store\_123. If specified, translation will search and read the required schema information from a metadata store in this dataset. If metadata store doesn't exist, translation will parse the metadata file and upload the schema info to a temp table in the dataset to speed up future translation jobs.

`  metadata_caching  `

`  MetadataCaching  `

Optional. Metadata caching settings. If specified, translation will cache the metadata. Otherwise, metadata will be parsed from the metadata file. The cache is stored on the service side. Hence, enabling this feature will store data from the provided metadata file on the service side for up to 7 days.

## SourceLocation

Represents one path to the location that holds source data.

Fields

Union field `  location  ` . The location of the source data. `  location  ` can be only one of the following:

`  gcs_path  `

`  string  `

The Cloud Storage path for a directory of files.

## SourceSpec

Represents one path to the location that holds source data.

Fields

`  encoding  `

`  string  `

Optional. The optional field to specify the encoding of the sql bytes.

Union field `  source  ` . The specific source SQL. `  source  ` can be only one of the following:

`  base_uri  `

`  string  `

The base URI for all files to be read in as sources for translation.

`  literal  `

`  Literal  `

Source literal.

## SourceTargetLocationMapping

Represents one mapping from a source location path to an optional target location path.

Fields

`  source_location  `

`  SourceLocation  `

The path to the location of the source data.

`  target_location  `

`  TargetLocation  `

The path to the location of the target data.

## SourceTargetMapping

Represents one mapping from a source SQL to a target SQL.

Fields

`  source_spec  `

`  SourceSpec  `

The source SQL or the path to it.

`  target_spec  `

`  TargetSpec  `

The target SQL or the path for it.

## SparkSQLDialect

This type has no fields.

The dialect definition for SparkSQL.

## StartMigrationWorkflowRequest

A request to start a previously created migration workflow.

Fields

`  name  `

`  string  `

Required. The unique identifier for the migration workflow. Example: `  projects/123/locations/us/workflows/1234  `

## TargetLocation

// Represents one path to the location that holds target data.

Fields

Union field `  location  ` . The location of the target data. `  location  ` can be only one of the following:

`  gcs_path  `

`  string  `

The Cloud Storage path for a directory of files.

## TargetSpec

Represents one path to the location that holds target data.

Fields

`  relative_path  `

`  string  `

The relative path for the target data. Given source file `  base_uri/input/sql  ` , the output would be `  target_base_uri/sql/relative_path/input.sql  ` .

## TeradataDialect

The dialect definition for Teradata.

Fields

`  mode  `

`  Mode  `

Which Teradata sub-dialect mode the user specifies.

## Mode

The sub-dialect options for Teradata.

Enums

`  MODE_UNSPECIFIED  `

Unspecified mode.

`  SQL  `

Teradata SQL mode.

`  BTEQ  `

BTEQ mode (which includes SQL).

## TeradataOptions

This type has no fields.

Teradata SQL specific translation task related settings.

## TimeInterval

A time interval extending just after a start time through an end time. If the start time is the same as the end time, then the interval represents a single point in time.

Fields

`  start_time  `

`  Timestamp  `

Optional. The beginning of the time interval. The default value for the start time is the end time. The start time must not be later than the end time.

`  end_time  `

`  Timestamp  `

Required. The end of the time interval.

## TimeSeries

The metrics object for a SubTask.

Fields

`  metric  `

`  string  `

Required. The name of the metric.

If the metric is not known by the service yet, it will be auto-created.

`  value_type  `

`  ValueType  `

Required. The value type of the time series.

`  metric_kind  `

`  MetricKind  `

Optional. The metric kind of the time series.

If present, it must be the same as the metric kind of the associated metric. If the associated metric's descriptor must be auto-created, then this field specifies the metric kind of the new descriptor and must be either `  GAUGE  ` (the default) or `  CUMULATIVE  ` .

`  points[]  `

`  Point  `

Required. The data points of this time series. When listing time series, points are returned in reverse time order.

When creating a time series, this field must contain exactly one point and the point's type must be the same as the value type of the associated metric. If the associated metric's descriptor must be auto-created, then the value type of the descriptor is determined by the point's type, which must be `  BOOL  ` , `  INT64  ` , `  DOUBLE  ` , or `  DISTRIBUTION  ` .

## TranslationConfigDetails

The translation config to capture necessary settings for a translation task and subtask.

Fields

`  source_dialect  `

`  Dialect  `

The dialect of the input files.

`  target_dialect  `

`  Dialect  `

The target dialect for the engine to translate the input to.

`  source_env  `

`  SourceEnv  `

The default source environment values for the translation.

`  source_target_location_mapping[]  `

`  SourceTargetLocationMapping  `

The mapping from source location paths to target location paths.

`  request_source  `

`  string  `

The indicator to show translation request initiator.

`  target_types[]  `

`  string  `

The types of output to generate, e.g. sql, metadata etc. If not specified, a default set of targets will be generated. Some additional target types may be slower to generate. See the documentation for the set of available target types.

Union field `  source_location  ` . The chosen path where the source for input files will be found. `  source_location  ` can be only one of the following:

`  gcs_source_path  `

`  string  `

The Cloud Storage path for a directory of files to translate in a task.

Union field `  target_location  ` . The chosen path where the destination for output files will be found. `  target_location  ` can be only one of the following:

`  gcs_target_path  `

`  string  `

The Cloud Storage path to write back the corresponding input files to.

Union field `  output_name_mapping  ` . The mapping of full SQL object names from their current state to the desired output. `  output_name_mapping  ` can be only one of the following:

`  name_mapping_list  `

`  ObjectNameMappingList  `

The mapping of objects to their desired output names in list form.

## TranslationDetails

The translation details to capture the necessary settings for a translation job.

Fields

`  source_target_mapping[]  `

`  SourceTargetMapping  `

The mapping from source to target SQL.

`  target_base_uri  `

`  string  `

The base URI for all writes to persistent storage.

`  source_environment  `

`  SourceEnvironment  `

The default source environment values for the translation.

`  target_return_literals[]  `

`  string  `

The list of literal targets that will be directly returned to the response. Each entry consists of the constructed path, EXCLUDING the base path. Not providing a target\_base\_uri will prevent writing to persistent storage.

`  target_types[]  `

`  string  `

The types of output to generate, e.g. sql, metadata, lineage\_from\_sql\_scripts, etc. If not specified, a default set of targets will be generated. Some additional target types may be slower to generate. See the documentation for the set of available target types.

## TranslationFileMapping

Mapping between an input and output file to be translated in a subtask.

Fields

`  input_path  `

`  string  `

The Cloud Storage path for a file to translation in a subtask.

`  output_path  `

`  string  `

The Cloud Storage path to write back the corresponding input file to.

## TranslationTaskDetails

The translation task config to capture necessary settings for a translation task and subtask.

Fields

`  input_path  `

`  string  `

The Cloud Storage path for translation input files.

`  output_path  `

`  string  `

The Cloud Storage path for translation output files.

`  file_paths[]  `

`  TranslationFileMapping  `

Cloud Storage files to be processed for translation.

`  schema_path  `

`  string  `

The Cloud Storage path to DDL files as table schema to assist semantic translation.

`  file_encoding  `

`  FileEncoding  `

The file encoding type.

`  identifier_settings  `

`  IdentifierSettings  `

The settings for SQL identifiers.

`  special_token_map  `

`  map<string, TokenType  ` \>

The map capturing special tokens to be replaced during translation. The key is special token in string. The value is the token data type. This is used to translate SQL query template which contains special token as place holder. The special token makes a query invalid to parse. This map will be applied to annotate those special token with types to let parser understand how to parse them into proper structure with type information.

`  filter  `

`  Filter  `

The filter applied to translation details.

`  translation_exception_table  `

`  string  `

Specifies the exact name of the bigquery table ("dataset.table") to be used for surfacing raw translation errors. If the table does not exist, we will create it. If it already exists and the schema is the same, we will re-use. If the table exists and the schema is different, we will throw an error.

Union field `  language_options  ` . The language specific settings for the translation task. `  language_options  ` can be only one of the following:

`  teradata_options  `

`  TeradataOptions  `

The Teradata SQL specific settings for the translation task.

`  bteq_options  `

`  BteqOptions  `

The BTEQ specific settings for the translation task.

## FileEncoding

The file encoding types.

Enums

`  FILE_ENCODING_UNSPECIFIED  `

File encoding setting is not specified.

`  UTF_8  `

File encoding is UTF\_8.

`  ISO_8859_1  `

File encoding is ISO\_8859\_1.

`  US_ASCII  `

File encoding is US\_ASCII.

`  UTF_16  `

File encoding is UTF\_16.

`  UTF_16LE  `

File encoding is UTF\_16LE.

`  UTF_16BE  `

File encoding is UTF\_16BE.

## TokenType

The special token data type.

Enums

`  TOKEN_TYPE_UNSPECIFIED  `

Token type is not specified.

`  STRING  `

Token type as string.

`  INT64  `

Token type as integer.

`  NUMERIC  `

Token type as numeric.

`  BOOL  `

Token type as boolean.

`  FLOAT64  `

Token type as float.

`  DATE  `

Token type as date.

`  TIMESTAMP  `

Token type as timestamp.

## TranslationTaskResult

Translation specific result details from the migration task.

Fields

`  translated_literals[]  `

`  Literal  `

The list of the translated literals.

`  report_log_messages[]  `

`  GcsReportLogMessage  `

The records from the aggregate CSV report for a migration workflow.

`  console_uri  `

`  string  `

The Cloud Console URI for the migration workflow.

## TypedValue

A single strongly-typed value.

Fields

Union field `  value  ` . The typed value field. `  value  ` can be only one of the following:

`  bool_value  `

`  bool  `

A Boolean value: `  true  ` or `  false  ` .

`  int64_value  `

`  int64  `

A 64-bit integer. Its range is approximately `  +/-9.2x10^18  ` .

`  double_value  `

`  double  `

A 64-bit double-precision floating-point number. Its magnitude is approximately `  +/-10^(+/-300)  ` and it has 16 significant digits of precision.

`  string_value  `

`  string  `

A variable-length string value.

`  distribution_value  `

`  Distribution  `

A distribution value.

## VerticaDialect

This type has no fields.

The dialect definition for Vertica.
