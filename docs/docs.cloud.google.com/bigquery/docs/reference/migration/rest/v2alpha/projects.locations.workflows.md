  - [Resource: MigrationWorkflow](#MigrationWorkflow)
      - [JSON representation](#MigrationWorkflow.SCHEMA_REPRESENTATION)
  - [MigrationTask](#MigrationTask)
      - [JSON representation](#MigrationTask.SCHEMA_REPRESENTATION)
  - [AssessmentTaskDetails](#AssessmentTaskDetails)
      - [JSON representation](#AssessmentTaskDetails.SCHEMA_REPRESENTATION)
  - [AssessmentFeatureHandle](#AssessmentFeatureHandle)
      - [JSON representation](#AssessmentFeatureHandle.SCHEMA_REPRESENTATION)
  - [TranslationTaskDetails](#TranslationTaskDetails)
      - [JSON representation](#TranslationTaskDetails.SCHEMA_REPRESENTATION)
  - [TeradataOptions](#TeradataOptions)
  - [BteqOptions](#BteqOptions)
      - [JSON representation](#BteqOptions.SCHEMA_REPRESENTATION)
  - [DatasetReference](#DatasetReference)
      - [JSON representation](#DatasetReference.SCHEMA_REPRESENTATION)
  - [TranslationFileMapping](#TranslationFileMapping)
      - [JSON representation](#TranslationFileMapping.SCHEMA_REPRESENTATION)
  - [FileEncoding](#FileEncoding)
  - [IdentifierSettings](#IdentifierSettings)
      - [JSON representation](#IdentifierSettings.SCHEMA_REPRESENTATION)
  - [IdentifierCase](#IdentifierCase)
  - [IdentifierRewriteMode](#IdentifierRewriteMode)
  - [TokenType](#TokenType)
  - [Filter](#Filter)
      - [JSON representation](#Filter.SCHEMA_REPRESENTATION)
  - [TranslationConfigDetails](#TranslationConfigDetails)
      - [JSON representation](#TranslationConfigDetails.SCHEMA_REPRESENTATION)
  - [ObjectNameMappingList](#ObjectNameMappingList)
      - [JSON representation](#ObjectNameMappingList.SCHEMA_REPRESENTATION)
  - [ObjectNameMapping](#ObjectNameMapping)
      - [JSON representation](#ObjectNameMapping.SCHEMA_REPRESENTATION)
  - [NameMappingKey](#NameMappingKey)
      - [JSON representation](#NameMappingKey.SCHEMA_REPRESENTATION)
  - [Type](#Type)
  - [NameMappingValue](#NameMappingValue)
      - [JSON representation](#NameMappingValue.SCHEMA_REPRESENTATION)
  - [Dialect](#Dialect)
      - [JSON representation](#Dialect.SCHEMA_REPRESENTATION)
  - [BigQueryDialect](#BigQueryDialect)
  - [HiveQLDialect](#HiveQLDialect)
  - [RedshiftDialect](#RedshiftDialect)
  - [TeradataDialect](#TeradataDialect)
      - [JSON representation](#TeradataDialect.SCHEMA_REPRESENTATION)
  - [Mode](#Mode)
  - [OracleDialect](#OracleDialect)
  - [SparkSQLDialect](#SparkSQLDialect)
  - [SnowflakeDialect](#SnowflakeDialect)
  - [NetezzaDialect](#NetezzaDialect)
  - [AzureSynapseDialect](#AzureSynapseDialect)
  - [VerticaDialect](#VerticaDialect)
  - [SQLServerDialect](#SQLServerDialect)
  - [PostgresqlDialect](#PostgresqlDialect)
  - [PrestoDialect](#PrestoDialect)
  - [MySQLDialect](#MySQLDialect)
  - [DB2Dialect](#DB2Dialect)
  - [SQLiteDialect](#SQLiteDialect)
  - [GreenplumDialect](#GreenplumDialect)
  - [SourceEnv](#SourceEnv)
      - [JSON representation](#SourceEnv.SCHEMA_REPRESENTATION)
  - [SourceTargetLocationMapping](#SourceTargetLocationMapping)
      - [JSON representation](#SourceTargetLocationMapping.SCHEMA_REPRESENTATION)
  - [SourceLocation](#SourceLocation)
      - [JSON representation](#SourceLocation.SCHEMA_REPRESENTATION)
  - [TargetLocation](#TargetLocation)
      - [JSON representation](#TargetLocation.SCHEMA_REPRESENTATION)
  - [TranslationDetails](#TranslationDetails)
      - [JSON representation](#TranslationDetails.SCHEMA_REPRESENTATION)
  - [SourceTargetMapping](#SourceTargetMapping)
      - [JSON representation](#SourceTargetMapping.SCHEMA_REPRESENTATION)
  - [SourceSpec](#SourceSpec)
      - [JSON representation](#SourceSpec.SCHEMA_REPRESENTATION)
  - [Literal](#Literal)
      - [JSON representation](#Literal.SCHEMA_REPRESENTATION)
  - [TargetSpec](#TargetSpec)
      - [JSON representation](#TargetSpec.SCHEMA_REPRESENTATION)
  - [SourceEnvironment](#SourceEnvironment)
      - [JSON representation](#SourceEnvironment.SCHEMA_REPRESENTATION)
  - [MetadataCaching](#MetadataCaching)
      - [JSON representation](#MetadataCaching.SCHEMA_REPRESENTATION)
  - [State](#State)
  - [MigrationTaskOrchestrationResult](#MigrationTaskOrchestrationResult)
      - [JSON representation](#MigrationTaskOrchestrationResult.SCHEMA_REPRESENTATION)
  - [AssessmentOrchestrationResultDetails](#AssessmentOrchestrationResultDetails)
      - [JSON representation](#AssessmentOrchestrationResultDetails.SCHEMA_REPRESENTATION)
  - [TranslationTaskResult](#TranslationTaskResult)
      - [JSON representation](#TranslationTaskResult.SCHEMA_REPRESENTATION)
  - [GcsReportLogMessage](#GcsReportLogMessage)
      - [JSON representation](#GcsReportLogMessage.SCHEMA_REPRESENTATION)
  - [MigrationTaskResult](#MigrationTaskResult)
      - [JSON representation](#MigrationTaskResult.SCHEMA_REPRESENTATION)
  - [State](#State_1)
  - [Methods](#METHODS_SUMMARY)

## Resource: MigrationWorkflow

A migration workflow which specifies what needs to be done for an EDW migration.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;name&quot;: string,
  &quot;displayName&quot;: string,
  &quot;tasks&quot;: {
    string: {
      object (MigrationTask)
    },
    ...
  },
  &quot;state&quot;: enum (State),
  &quot;createTime&quot;: string,
  &quot;lastUpdateTime&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  name  `

`  string  `

Output only. Immutable. Identifier. The unique identifier for the migration workflow. The ID is server-generated.

Example: `  projects/123/locations/us/workflows/345  `

`  displayName  `

`  string  `

The display name of the workflow. This can be set to give a workflow a descriptive name. There is no guarantee or enforcement of uniqueness.

`  tasks  `

`  map (key: string, value: object ( MigrationTask  ` ))

The tasks in a workflow in a named map. The name (i.e. key) has no meaning and is merely a convenient way to address a specific task in a workflow.

`  state  `

`  enum ( State  ` )

Output only. That status of the workflow.

`  createTime  `

`  string ( Timestamp  ` format)

Output only. Time when the workflow was created.

`  lastUpdateTime  `

`  string ( Timestamp  ` format)

Output only. Time when the workflow was last updated.

## MigrationTask

A single task for a migration which has details about the configuration of the task.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;id&quot;: string,
  &quot;type&quot;: string,
  &quot;details&quot;: {
    &quot;@type&quot;: string,
    field1: ...,
    ...
  },
  &quot;state&quot;: enum (State),
  &quot;processingError&quot;: {
    object (ErrorInfo)
  },
  &quot;createTime&quot;: string,
  &quot;lastUpdateTime&quot;: string,
  &quot;orchestrationResult&quot;: {
    object (MigrationTaskOrchestrationResult)
  },
  &quot;resourceErrorDetails&quot;: [
    {
      object (ResourceErrorDetail)
    }
  ],
  &quot;resourceErrorCount&quot;: integer,
  &quot;metrics&quot;: [
    {
      object (TimeSeries)
    }
  ],
  &quot;taskResult&quot;: {
    object (MigrationTaskResult)
  },
  &quot;totalProcessingErrorCount&quot;: integer,
  &quot;totalResourceErrorCount&quot;: integer,

  // Union field task_details can be only one of the following:
  &quot;assessmentTaskDetails&quot;: {
    object (AssessmentTaskDetails)
  },
  &quot;translationTaskDetails&quot;: {
    object (TranslationTaskDetails)
  },
  &quot;translationConfigDetails&quot;: {
    object (TranslationConfigDetails)
  },
  &quot;translationDetails&quot;: {
    object (TranslationDetails)
  }
  // End of list of possible types for union field task_details.
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  id  `

`  string  `

Output only. Immutable. The unique identifier for the migration task. The ID is server-generated.

`  type  `

`  string  `

The type of the task. This must be one of the supported task types: Translation\_Teradata2BQ, Translation\_Redshift2BQ, Translation\_Bteq2BQ, Translation\_Oracle2BQ, Translation\_HiveQL2BQ, Translation\_SparkSQL2BQ, Translation\_Snowflake2BQ, Translation\_Netezza2BQ, Translation\_AzureSynapse2BQ, Translation\_Vertica2BQ, Translation\_SQLServer2BQ, Translation\_Presto2BQ, Translation\_MySQL2BQ, Translation\_Postgresql2BQ, Translation\_SQLite2BQ, Translation\_Greenplum2BQ.

`  details  `

`  object  `

DEPRECATED\! Use one of the task\_details below. The details of the task. The type URL must be one of the supported task details messages and correspond to the Task's type.

`  state  `

`  enum ( State  ` )

Output only. The current state of the task.

`  processingError  `

`  object ( ErrorInfo  ` )

Output only. An explanation that may be populated when the task is in FAILED state.

`  createTime  `

`  string ( Timestamp  ` format)

Output only. Time when the task was created.

`  lastUpdateTime  `

`  string ( Timestamp  ` format)

Output only. Time when the task was last updated.

`  orchestrationResult (deprecated)  `

`  object ( MigrationTaskOrchestrationResult  ` )

This item is deprecated\!

Output only. Deprecated: Use the taskResult field below instead. Additional information about the orchestration.

`  resourceErrorDetails[]  `

`  object ( ResourceErrorDetail  ` )

Output only. Provides details to errors and issues encountered while processing the task. Presence of error details does not mean that the task failed.

`  resourceErrorCount  `

`  integer  `

The number or resources with errors. Note: This is not the total number of errors as each resource can have more than one error. This is used to indicate truncation by having a `  resourceErrorCount  ` that is higher than the size of `  resourceErrorDetails  ` .

`  metrics[]  `

`  object ( TimeSeries  ` )

Output only. The metrics for the task.

`  taskResult  `

`  object ( MigrationTaskResult  ` )

Output only. The result of the task.

`  totalProcessingErrorCount  `

`  integer  `

Output only. Count of all the processing errors in this task and its subtasks.

`  totalResourceErrorCount  `

`  integer  `

Output only. Count of all the resource errors in this task and its subtasks.

Union field `  task_details  ` . The details of the task. `  task_details  ` can be only one of the following:

`  assessmentTaskDetails  `

`  object ( AssessmentTaskDetails  ` )

Task configuration for Assessment.

`  translationTaskDetails  `

`  object ( TranslationTaskDetails  ` )

Task configuration for Batch SQL Translation.

`  translationConfigDetails  `

`  object ( TranslationConfigDetails  ` )

Task configuration for CW Batch/Offline SQL Translation.

`  translationDetails  `

`  object ( TranslationDetails  ` )

Task details for unified SQL Translation.

## AssessmentTaskDetails

Assessment task config.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;inputPath&quot;: string,
  &quot;outputDataset&quot;: string,
  &quot;querylogsPath&quot;: string,
  &quot;dataSource&quot;: string,
  &quot;featureHandle&quot;: {
    object (AssessmentFeatureHandle)
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  inputPath  `

`  string  `

Required. The Cloud Storage path for assessment input files.

`  outputDataset  `

`  string  `

Required. The BigQuery dataset for output.

`  querylogsPath  `

`  string  `

Optional. An optional Cloud Storage path to write the query logs (which is then used as an input path on the translation task)

`  dataSource  `

`  string  `

Required. The data source or data warehouse type (eg: TERADATA/REDSHIFT) from which the input data is extracted.

`  featureHandle  `

`  object ( AssessmentFeatureHandle  ` )

Optional. A collection of additional feature flags for this assessment.

## AssessmentFeatureHandle

User-definable feature flags for assessment tasks.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;addShareableDataset&quot;: boolean
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  addShareableDataset  `

`  boolean  `

Optional. Whether to create a dataset containing non-PII data in addition to the output dataset.

## TranslationTaskDetails

The translation task config to capture necessary settings for a translation task and subtask.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;inputPath&quot;: string,
  &quot;outputPath&quot;: string,
  &quot;filePaths&quot;: [
    {
      object (TranslationFileMapping)
    }
  ],
  &quot;schemaPath&quot;: string,
  &quot;fileEncoding&quot;: enum (FileEncoding),
  &quot;identifierSettings&quot;: {
    object (IdentifierSettings)
  },
  &quot;specialTokenMap&quot;: {
    string: enum (TokenType),
    ...
  },
  &quot;filter&quot;: {
    object (Filter)
  },
  &quot;translationExceptionTable&quot;: string,

  // Union field language_options can be only one of the following:
  &quot;teradataOptions&quot;: {
    object (TeradataOptions)
  },
  &quot;bteqOptions&quot;: {
    object (BteqOptions)
  }
  // End of list of possible types for union field language_options.
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  inputPath  `

`  string  `

The Cloud Storage path for translation input files.

`  outputPath  `

`  string  `

The Cloud Storage path for translation output files.

`  filePaths[]  `

`  object ( TranslationFileMapping  ` )

Cloud Storage files to be processed for translation.

`  schemaPath  `

`  string  `

The Cloud Storage path to DDL files as table schema to assist semantic translation.

`  fileEncoding  `

`  enum ( FileEncoding  ` )

The file encoding type.

`  identifierSettings  `

`  object ( IdentifierSettings  ` )

The settings for SQL identifiers.

`  specialTokenMap  `

`  map (key: string, value: enum ( TokenType  ` ))

The map capturing special tokens to be replaced during translation. The key is special token in string. The value is the token data type. This is used to translate SQL query template which contains special token as place holder. The special token makes a query invalid to parse. This map will be applied to annotate those special token with types to let parser understand how to parse them into proper structure with type information.

`  filter  `

`  object ( Filter  ` )

The filter applied to translation details.

`  translationExceptionTable  `

`  string  `

Specifies the exact name of the bigquery table ("dataset.table") to be used for surfacing raw translation errors. If the table does not exist, we will create it. If it already exists and the schema is the same, we will re-use. If the table exists and the schema is different, we will throw an error.

Union field `  language_options  ` . The language specific settings for the translation task. `  language_options  ` can be only one of the following:

`  teradataOptions  `

`  object ( TeradataOptions  ` )

The Teradata SQL specific settings for the translation task.

`  bteqOptions  `

`  object ( BteqOptions  ` )

The BTEQ specific settings for the translation task.

## TeradataOptions

This type has no fields.

Teradata SQL specific translation task related settings.

## BteqOptions

BTEQ translation task related settings.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;projectDataset&quot;: {
    object (DatasetReference)
  },
  &quot;defaultPathUri&quot;: string,
  &quot;fileReplacementMap&quot;: {
    string: string,
    ...
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  projectDataset  `

`  object ( DatasetReference  ` )

Specifies the project and dataset in BigQuery that will be used for external table creation during the translation.

`  defaultPathUri  `

`  string  `

The Cloud Storage location to be used as the default path for files that are not otherwise specified in the file replacement map.

`  fileReplacementMap  `

`  map (key: string, value: string)  `

Maps the local paths that are used in BTEQ scripts (the keys) to the paths in Cloud Storage that should be used in their stead in the translation (the value).

## DatasetReference

Reference to a BigQuery dataset.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;datasetId&quot;: string,
  &quot;projectId&quot;: string,
  &quot;datasetIdAlternative&quot;: [
    string
  ],
  &quot;projectIdAlternative&quot;: [
    string
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  datasetId  `

`  string  `

A unique ID for this dataset, without the project name. The ID must contain only letters (a-z, A-Z), numbers (0-9), or underscores (\_). The maximum length is 1,024 characters.

`  projectId  `

`  string  `

The ID of the project containing this dataset.

`  datasetIdAlternative[]  `

`  string  `

The alternative field that will be used when the service is not able to translate the received data to the datasetId field.

`  projectIdAlternative[]  `

`  string  `

The alternative field that will be used when the service is not able to translate the received data to the projectId field.

## TranslationFileMapping

Mapping between an input and output file to be translated in a subtask.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;inputPath&quot;: string,
  &quot;outputPath&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  inputPath  `

`  string  `

The Cloud Storage path for a file to translation in a subtask.

`  outputPath  `

`  string  `

The Cloud Storage path to write back the corresponding input file to.

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

## IdentifierSettings

Settings related to SQL identifiers.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;outputIdentifierCase&quot;: enum (IdentifierCase),
  &quot;identifierRewriteMode&quot;: enum (IdentifierRewriteMode)
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  outputIdentifierCase  `

`  enum ( IdentifierCase  ` )

The setting to control output queries' identifier case.

`  identifierRewriteMode  `

`  enum ( IdentifierRewriteMode  ` )

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

## Filter

The filter applied to fields of translation details.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;inputFileExclusionPrefixes&quot;: [
    string
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  inputFileExclusionPrefixes[]  `

`  string  `

The list of prefixes used to exclude processing for input files.

## TranslationConfigDetails

The translation config to capture necessary settings for a translation task and subtask.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;sourceDialect&quot;: {
    object (Dialect)
  },
  &quot;targetDialect&quot;: {
    object (Dialect)
  },
  &quot;sourceEnv&quot;: {
    object (SourceEnv)
  },
  &quot;sourceTargetLocationMapping&quot;: [
    {
      object (SourceTargetLocationMapping)
    }
  ],
  &quot;requestSource&quot;: string,
  &quot;targetTypes&quot;: [
    string
  ],

  // Union field source_location can be only one of the following:
  &quot;gcsSourcePath&quot;: string
  // End of list of possible types for union field source_location.

  // Union field target_location can be only one of the following:
  &quot;gcsTargetPath&quot;: string
  // End of list of possible types for union field target_location.

  // Union field output_name_mapping can be only one of the following:
  &quot;nameMappingList&quot;: {
    object (ObjectNameMappingList)
  }
  // End of list of possible types for union field output_name_mapping.
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  sourceDialect  `

`  object ( Dialect  ` )

The dialect of the input files.

`  targetDialect  `

`  object ( Dialect  ` )

The target dialect for the engine to translate the input to.

`  sourceEnv  `

`  object ( SourceEnv  ` )

The default source environment values for the translation.

`  sourceTargetLocationMapping[]  `

`  object ( SourceTargetLocationMapping  ` )

The mapping from source location paths to target location paths.

`  requestSource  `

`  string  `

The indicator to show translation request initiator.

`  targetTypes[]  `

`  string  `

The types of output to generate, e.g. sql, metadata etc. If not specified, a default set of targets will be generated. Some additional target types may be slower to generate. See the documentation for the set of available target types.

Union field `  source_location  ` . The chosen path where the source for input files will be found. `  source_location  ` can be only one of the following:

`  gcsSourcePath  `

`  string  `

The Cloud Storage path for a directory of files to translate in a task.

Union field `  target_location  ` . The chosen path where the destination for output files will be found. `  target_location  ` can be only one of the following:

`  gcsTargetPath  `

`  string  `

The Cloud Storage path to write back the corresponding input files to.

Union field `  output_name_mapping  ` . The mapping of full SQL object names from their current state to the desired output. `  output_name_mapping  ` can be only one of the following:

`  nameMappingList  `

`  object ( ObjectNameMappingList  ` )

The mapping of objects to their desired output names in list form.

## ObjectNameMappingList

Represents a map of name mappings using a list of key:value proto messages of existing name to desired output name.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;nameMap&quot;: [
    {
      object (ObjectNameMapping)
    }
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  nameMap[]  `

`  object ( ObjectNameMapping  ` )

The elements of the object name map.

## ObjectNameMapping

Represents a key-value pair of NameMappingKey to NameMappingValue to represent the mapping of SQL names from the input value to desired output.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;source&quot;: {
    object (NameMappingKey)
  },
  &quot;target&quot;: {
    object (NameMappingValue)
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  source  `

`  object ( NameMappingKey  ` )

The name of the object in source that is being mapped.

`  target  `

`  object ( NameMappingValue  ` )

The desired target name of the object that is being mapped.

## NameMappingKey

The potential components of a full name mapping that will be mapped during translation in the source data warehouse.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;type&quot;: enum (Type),
  &quot;database&quot;: string,
  &quot;schema&quot;: string,
  &quot;relation&quot;: string,
  &quot;attribute&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  type  `

`  enum ( Type  ` )

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

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;database&quot;: string,
  &quot;schema&quot;: string,
  &quot;relation&quot;: string,
  &quot;attribute&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

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

## Dialect

The possible dialect options for translation.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{

  // Union field dialect_value can be only one of the following:
  &quot;bigqueryDialect&quot;: {
    object (BigQueryDialect)
  },
  &quot;hiveqlDialect&quot;: {
    object (HiveQLDialect)
  },
  &quot;redshiftDialect&quot;: {
    object (RedshiftDialect)
  },
  &quot;teradataDialect&quot;: {
    object (TeradataDialect)
  },
  &quot;oracleDialect&quot;: {
    object (OracleDialect)
  },
  &quot;sparksqlDialect&quot;: {
    object (SparkSQLDialect)
  },
  &quot;snowflakeDialect&quot;: {
    object (SnowflakeDialect)
  },
  &quot;netezzaDialect&quot;: {
    object (NetezzaDialect)
  },
  &quot;azureSynapseDialect&quot;: {
    object (AzureSynapseDialect)
  },
  &quot;verticaDialect&quot;: {
    object (VerticaDialect)
  },
  &quot;sqlServerDialect&quot;: {
    object (SQLServerDialect)
  },
  &quot;postgresqlDialect&quot;: {
    object (PostgresqlDialect)
  },
  &quot;prestoDialect&quot;: {
    object (PrestoDialect)
  },
  &quot;mysqlDialect&quot;: {
    object (MySQLDialect)
  },
  &quot;db2Dialect&quot;: {
    object (DB2Dialect)
  },
  &quot;sqliteDialect&quot;: {
    object (SQLiteDialect)
  },
  &quot;greenplumDialect&quot;: {
    object (GreenplumDialect)
  }
  // End of list of possible types for union field dialect_value.
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `  dialect_value  ` . The possible dialect options that this message represents. `  dialect_value  ` can be only one of the following:

`  bigqueryDialect  `

`  object ( BigQueryDialect  ` )

The BigQuery dialect

`  hiveqlDialect  `

`  object ( HiveQLDialect  ` )

The HiveQL dialect

`  redshiftDialect  `

`  object ( RedshiftDialect  ` )

The Redshift dialect

`  teradataDialect  `

`  object ( TeradataDialect  ` )

The Teradata dialect

`  oracleDialect  `

`  object ( OracleDialect  ` )

The Oracle dialect

`  sparksqlDialect  `

`  object ( SparkSQLDialect  ` )

The SparkSQL dialect

`  snowflakeDialect  `

`  object ( SnowflakeDialect  ` )

The Snowflake dialect

`  netezzaDialect  `

`  object ( NetezzaDialect  ` )

The Netezza dialect

`  azureSynapseDialect  `

`  object ( AzureSynapseDialect  ` )

The Azure Synapse dialect

`  verticaDialect  `

`  object ( VerticaDialect  ` )

The Vertica dialect

`  sqlServerDialect  `

`  object ( SQLServerDialect  ` )

The SQL Server dialect

`  postgresqlDialect  `

`  object ( PostgresqlDialect  ` )

The Postgresql dialect

`  prestoDialect  `

`  object ( PrestoDialect  ` )

The Presto dialect

`  mysqlDialect  `

`  object ( MySQLDialect  ` )

The MySQL dialect

`  db2Dialect  `

`  object ( DB2Dialect  ` )

DB2 dialect

`  sqliteDialect  `

`  object ( SQLiteDialect  ` )

SQLite dialect

`  greenplumDialect  `

`  object ( GreenplumDialect  ` )

Greenplum dialect

## BigQueryDialect

This type has no fields.

The dialect definition for BigQuery.

## HiveQLDialect

This type has no fields.

The dialect definition for HiveQL.

## RedshiftDialect

This type has no fields.

The dialect definition for Redshift.

## TeradataDialect

The dialect definition for Teradata.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;mode&quot;: enum (Mode)
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  mode  `

`  enum ( Mode  ` )

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

## OracleDialect

This type has no fields.

The dialect definition for Oracle.

## SparkSQLDialect

This type has no fields.

The dialect definition for SparkSQL.

## SnowflakeDialect

This type has no fields.

The dialect definition for Snowflake.

## NetezzaDialect

This type has no fields.

The dialect definition for Netezza.

## AzureSynapseDialect

This type has no fields.

The dialect definition for Azure Synapse.

## VerticaDialect

This type has no fields.

The dialect definition for Vertica.

## SQLServerDialect

This type has no fields.

The dialect definition for SQL Server.

## PostgresqlDialect

This type has no fields.

The dialect definition for Postgresql.

## PrestoDialect

This type has no fields.

The dialect definition for Presto.

## MySQLDialect

This type has no fields.

The dialect definition for MySQL.

## DB2Dialect

This type has no fields.

The dialect definition for DB2.

## SQLiteDialect

This type has no fields.

The dialect definition for SQLite.

## GreenplumDialect

This type has no fields.

The dialect definition for Greenplum.

## SourceEnv

Represents the default source environment values for the translation.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;defaultDatabase&quot;: string,
  &quot;schemaSearchPath&quot;: [
    string
  ],
  &quot;metadataStoreDataset&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  defaultDatabase  `

`  string  `

The default database name to fully qualify SQL objects when their database name is missing.

`  schemaSearchPath[]  `

`  string  `

The schema search path. When SQL objects are missing schema name, translation engine will search through this list to find the value.

`  metadataStoreDataset  `

`  string  `

Optional. Expects a valid BigQuery dataset ID that exists, e.g., project-123.metadata\_store\_123. If specified, translation will search and read the required schema information from a metadata store in this dataset. If metadata store doesn't exist, translation will parse the metadata file and upload the schema info to a temp table in the dataset to speed up future translation jobs.

## SourceTargetLocationMapping

Represents one mapping from a source location path to an optional target location path.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;sourceLocation&quot;: {
    object (SourceLocation)
  },
  &quot;targetLocation&quot;: {
    object (TargetLocation)
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  sourceLocation  `

`  object ( SourceLocation  ` )

The path to the location of the source data.

`  targetLocation  `

`  object ( TargetLocation  ` )

The path to the location of the target data.

## SourceLocation

Represents one path to the location that holds source data.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{

  // Union field location can be only one of the following:
  &quot;gcsPath&quot;: string
  // End of list of possible types for union field location.
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `  location  ` . The location of the source data. `  location  ` can be only one of the following:

`  gcsPath  `

`  string  `

The Cloud Storage path for a directory of files.

## TargetLocation

// Represents one path to the location that holds target data.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{

  // Union field location can be only one of the following:
  &quot;gcsPath&quot;: string
  // End of list of possible types for union field location.
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `  location  ` . The location of the target data. `  location  ` can be only one of the following:

`  gcsPath  `

`  string  `

The Cloud Storage path for a directory of files.

## TranslationDetails

The translation details to capture the necessary settings for a translation job.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;sourceTargetMapping&quot;: [
    {
      object (SourceTargetMapping)
    }
  ],
  &quot;targetBaseUri&quot;: string,
  &quot;sourceEnvironment&quot;: {
    object (SourceEnvironment)
  },
  &quot;targetReturnLiterals&quot;: [
    string
  ],
  &quot;targetTypes&quot;: [
    string
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  sourceTargetMapping[]  `

`  object ( SourceTargetMapping  ` )

The mapping from source to target SQL.

`  targetBaseUri  `

`  string  `

The base URI for all writes to persistent storage.

`  sourceEnvironment  `

`  object ( SourceEnvironment  ` )

The default source environment values for the translation.

`  targetReturnLiterals[]  `

`  string  `

The list of literal targets that will be directly returned to the response. Each entry consists of the constructed path, EXCLUDING the base path. Not providing a targetBaseUri will prevent writing to persistent storage.

`  targetTypes[]  `

`  string  `

The types of output to generate, e.g. sql, metadata, lineage\_from\_sql\_scripts, etc. If not specified, a default set of targets will be generated. Some additional target types may be slower to generate. See the documentation for the set of available target types.

## SourceTargetMapping

Represents one mapping from a source SQL to a target SQL.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;sourceSpec&quot;: {
    object (SourceSpec)
  },
  &quot;targetSpec&quot;: {
    object (TargetSpec)
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  sourceSpec  `

`  object ( SourceSpec  ` )

The source SQL or the path to it.

`  targetSpec  `

`  object ( TargetSpec  ` )

The target SQL or the path for it.

## SourceSpec

Represents one path to the location that holds source data.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;encoding&quot;: string,

  // Union field source can be only one of the following:
  &quot;baseUri&quot;: string,
  &quot;literal&quot;: {
    object (Literal)
  }
  // End of list of possible types for union field source.
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  encoding  `

`  string  `

Optional. The optional field to specify the encoding of the sql bytes.

Union field `  source  ` . The specific source SQL. `  source  ` can be only one of the following:

`  baseUri  `

`  string  `

The base URI for all files to be read in as sources for translation.

`  literal  `

`  object ( Literal  ` )

Source literal.

## Literal

Literal data.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;relativePath&quot;: string,

  // Union field literal_data can be only one of the following:
  &quot;literalString&quot;: string,
  &quot;literalBytes&quot;: string
  // End of list of possible types for union field literal_data.
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  relativePath  `

`  string  `

Required. The identifier of the literal entry.

Union field `  literal_data  ` . The literal SQL contents. `  literal_data  ` can be only one of the following:

`  literalString  `

`  string  `

Literal string data.

`  literalBytes  `

`  string ( bytes format)  `

Literal byte data.

## TargetSpec

Represents one path to the location that holds target data.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;relativePath&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  relativePath  `

`  string  `

The relative path for the target data. Given source file `  baseUri/input/sql  ` , the output would be `  targetBaseUri/sql/relativePath/input.sql  ` .

## SourceEnvironment

Represents the default source environment values for the translation.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;defaultDatabase&quot;: string,
  &quot;schemaSearchPath&quot;: [
    string
  ],
  &quot;metadataStoreDataset&quot;: string,
  &quot;metadataCaching&quot;: {
    object (MetadataCaching)
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  defaultDatabase  `

`  string  `

The default database name to fully qualify SQL objects when their database name is missing.

`  schemaSearchPath[]  `

`  string  `

The schema search path. When SQL objects are missing schema name, translation engine will search through this list to find the value.

`  metadataStoreDataset  `

`  string  `

Optional. Expects a validQ BigQuery dataset ID that exists, e.g., project-123.metadata\_store\_123. If specified, translation will search and read the required schema information from a metadata store in this dataset. If metadata store doesn't exist, translation will parse the metadata file and upload the schema info to a temp table in the dataset to speed up future translation jobs.

`  metadataCaching  `

`  object ( MetadataCaching  ` )

Optional. Metadata caching settings. If specified, translation will cache the metadata. Otherwise, metadata will be parsed from the metadata file. The cache is stored on the service side. Hence, enabling this feature will store data from the provided metadata file on the service side for up to 7 days.

## MetadataCaching

Metadata caching settings.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;maxCacheAge&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  maxCacheAge  `

`  string ( Duration  ` format)

Optional. The maximum age of the metadata cache. If the cache is older than this value, the cache will be refreshed. A cache will not be kept for longer than 7 days. Providing no value or a value larger than 7 days will result in using the cache if available (i.e. the same as setting the value to 7 days).

Setting the duration to 0 or a negative value will refresh the cache.

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

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{

  // Union field details can be only one of the following:
  &quot;assessmentDetails&quot;: {
    object (AssessmentOrchestrationResultDetails)
  },
  &quot;translationTaskResult&quot;: {
    object (TranslationTaskResult)
  }
  // End of list of possible types for union field details.
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `  details  ` . Details specific to the task type. `  details  ` can be only one of the following:

`  assessmentDetails  `

`  object ( AssessmentOrchestrationResultDetails  ` )

Details specific to assessment task types.

`  translationTaskResult  `

`  object ( TranslationTaskResult  ` )

Details specific to translation task types.

## AssessmentOrchestrationResultDetails

Details for an assessment task orchestration result.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;outputTablesSchemaVersion&quot;: string,
  &quot;reportUri&quot;: string,
  &quot;additionalReportUris&quot;: {
    string: string,
    ...
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  outputTablesSchemaVersion  `

`  string  `

Optional. The version used for the output table schemas.

`  reportUri  `

`  string  `

Optional. The URI of the Data Studio report.

`  additionalReportUris  `

`  map (key: string, value: string)  `

Optional. Mapping with additional report URIs. This gives a mapping of report names to their URIs. The possible values for the keys are documented in the user guide.

## TranslationTaskResult

Translation specific result details from the migration task.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;translatedLiterals&quot;: [
    {
      object (Literal)
    }
  ],
  &quot;reportLogMessages&quot;: [
    {
      object (GcsReportLogMessage)
    }
  ],
  &quot;consoleUri&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  translatedLiterals[]  `

`  object ( Literal  ` )

The list of the translated literals.

`  reportLogMessages[]  `

`  object ( GcsReportLogMessage  ` )

The records from the aggregate CSV report for a migration workflow.

`  consoleUri  `

`  string  `

The Cloud Console URI for the migration workflow.

## GcsReportLogMessage

A record in the aggregate CSV report for a migration workflow

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;severity&quot;: string,
  &quot;category&quot;: string,
  &quot;filePath&quot;: string,
  &quot;filename&quot;: string,
  &quot;sourceScriptLine&quot;: integer,
  &quot;sourceScriptColumn&quot;: integer,
  &quot;message&quot;: string,
  &quot;scriptContext&quot;: string,
  &quot;action&quot;: string,
  &quot;effect&quot;: string,
  &quot;objectName&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  severity  `

`  string  `

Severity of the translation record.

`  category  `

`  string  `

Category of the error/warning. Example: SyntaxError

`  filePath  `

`  string  `

The file path in which the error occurred

`  filename  `

`  string  `

The file name in which the error occurred

`  sourceScriptLine  `

`  integer  `

Specifies the row from the source text where the error occurred (0 based, -1 for messages without line location). Example: 2

`  sourceScriptColumn  `

`  integer  `

Specifies the column from the source texts where the error occurred. (0 based, -1 for messages without column location) example: 6

`  message  `

`  string  `

Detailed message of the record.

`  scriptContext  `

`  string  `

The script context (obfuscated) in which the error occurred

`  action  `

`  string  `

Category of the error/warning. Example: SyntaxError

`  effect  `

`  string  `

Effect of the error/warning. Example: COMPATIBILITY

`  objectName  `

`  string  `

Name of the affected object in the log message.

## MigrationTaskResult

The migration task result.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{

  // Union field details can be only one of the following:
  &quot;assessmentDetails&quot;: {
    object (AssessmentOrchestrationResultDetails)
  },
  &quot;translationTaskResult&quot;: {
    object (TranslationTaskResult)
  }
  // End of list of possible types for union field details.
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `  details  ` . Details specific to the task type. `  details  ` can be only one of the following:

`  assessmentDetails  `

`  object ( AssessmentOrchestrationResultDetails  ` )

Details specific to assessment task types.

`  translationTaskResult  `

`  object ( TranslationTaskResult  ` )

Details specific to translation task types.

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

## Methods

### `             create           `

Creates a migration workflow.

### `             delete           `

Deletes a migration workflow by name.

### `             get           `

Gets a previously created migration workflow.

### `             list           `

Lists previously created migration workflow.

### `             start           `

Starts a previously created migration workflow.
