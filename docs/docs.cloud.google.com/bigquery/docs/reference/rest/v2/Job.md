  - [JSON representation](#SCHEMA_REPRESENTATION)
  - [JobConfiguration](#JobConfiguration)
      - [JSON representation](#JobConfiguration.SCHEMA_REPRESENTATION)
  - [JobConfigurationQuery](#JobConfigurationQuery)
      - [JSON representation](#JobConfigurationQuery.SCHEMA_REPRESENTATION)
  - [SystemVariables](#SystemVariables)
      - [JSON representation](#SystemVariables.SCHEMA_REPRESENTATION)
  - [ScriptOptions](#ScriptOptions)
      - [JSON representation](#ScriptOptions.SCHEMA_REPRESENTATION)
  - [KeyResultStatementKind](#KeyResultStatementKind)
  - [JobConfigurationLoad](#JobConfigurationLoad)
      - [JSON representation](#JobConfigurationLoad.SCHEMA_REPRESENTATION)
  - [DestinationTableProperties](#DestinationTableProperties)
      - [JSON representation](#DestinationTableProperties.SCHEMA_REPRESENTATION)
  - [ColumnNameCharacterMap](#ColumnNameCharacterMap)
  - [SourceColumnMatch](#SourceColumnMatch)
  - [JobConfigurationTableCopy](#JobConfigurationTableCopy)
      - [JSON representation](#JobConfigurationTableCopy.SCHEMA_REPRESENTATION)
  - [OperationType](#OperationType)
  - [JobConfigurationExtract](#JobConfigurationExtract)
      - [JSON representation](#JobConfigurationExtract.SCHEMA_REPRESENTATION)
  - [ModelExtractOptions](#ModelExtractOptions)
      - [JSON representation](#ModelExtractOptions.SCHEMA_REPRESENTATION)
  - [JobStatistics](#JobStatistics)
      - [JSON representation](#JobStatistics.SCHEMA_REPRESENTATION)
  - [JobStatistics2](#JobStatistics2)
      - [JSON representation](#JobStatistics2.SCHEMA_REPRESENTATION)
  - [ExplainQueryStage](#ExplainQueryStage)
      - [JSON representation](#ExplainQueryStage.SCHEMA_REPRESENTATION)
  - [ExplainQueryStep](#ExplainQueryStep)
      - [JSON representation](#ExplainQueryStep.SCHEMA_REPRESENTATION)
  - [ComputeMode](#ComputeMode)
  - [QueryTimelineSample](#QueryTimelineSample)
      - [JSON representation](#QueryTimelineSample.SCHEMA_REPRESENTATION)
  - [MlStatistics](#MlStatistics)
      - [JSON representation](#MlStatistics.SCHEMA_REPRESENTATION)
  - [TrainingType](#TrainingType)
  - [ExportDataStatistics](#ExportDataStatistics)
      - [JSON representation](#ExportDataStatistics.SCHEMA_REPRESENTATION)
  - [ExternalServiceCost](#ExternalServiceCost)
      - [JSON representation](#ExternalServiceCost.SCHEMA_REPRESENTATION)
  - [BiEngineStatistics](#BiEngineStatistics)
      - [JSON representation](#BiEngineStatistics.SCHEMA_REPRESENTATION)
  - [BiEngineMode](#BiEngineMode)
  - [BiEngineAccelerationMode](#BiEngineAccelerationMode)
  - [BiEngineReason](#BiEngineReason)
      - [JSON representation](#BiEngineReason.SCHEMA_REPRESENTATION)
  - [Code](#Code)
  - [LoadQueryStatistics](#LoadQueryStatistics)
      - [JSON representation](#LoadQueryStatistics.SCHEMA_REPRESENTATION)
  - [SearchStatistics](#SearchStatistics)
      - [JSON representation](#SearchStatistics.SCHEMA_REPRESENTATION)
  - [IndexUsageMode](#IndexUsageMode)
  - [IndexUnusedReason](#IndexUnusedReason)
      - [JSON representation](#IndexUnusedReason.SCHEMA_REPRESENTATION)
  - [Code](#Code_1)
  - [VectorSearchStatistics](#VectorSearchStatistics)
      - [JSON representation](#VectorSearchStatistics.SCHEMA_REPRESENTATION)
  - [IndexUsageMode](#IndexUsageMode_1)
  - [StoredColumnsUsage](#StoredColumnsUsage)
      - [JSON representation](#StoredColumnsUsage.SCHEMA_REPRESENTATION)
  - [StoredColumnsUnusedReason](#StoredColumnsUnusedReason)
      - [JSON representation](#StoredColumnsUnusedReason.SCHEMA_REPRESENTATION)
  - [Code](#Code_2)
  - [PerformanceInsights](#PerformanceInsights)
      - [JSON representation](#PerformanceInsights.SCHEMA_REPRESENTATION)
  - [StagePerformanceStandaloneInsight](#StagePerformanceStandaloneInsight)
      - [JSON representation](#StagePerformanceStandaloneInsight.SCHEMA_REPRESENTATION)
  - [HighCardinalityJoin](#HighCardinalityJoin)
      - [JSON representation](#HighCardinalityJoin.SCHEMA_REPRESENTATION)
  - [PartitionSkew](#PartitionSkew)
      - [JSON representation](#PartitionSkew.SCHEMA_REPRESENTATION)
  - [SkewSource](#SkewSource)
      - [JSON representation](#SkewSource.SCHEMA_REPRESENTATION)
  - [StagePerformanceChangeInsight](#StagePerformanceChangeInsight)
      - [JSON representation](#StagePerformanceChangeInsight.SCHEMA_REPRESENTATION)
  - [InputDataChange](#InputDataChange)
      - [JSON representation](#InputDataChange.SCHEMA_REPRESENTATION)
  - [QueryInfo](#QueryInfo)
      - [JSON representation](#QueryInfo.SCHEMA_REPRESENTATION)
  - [SparkStatistics](#SparkStatistics)
      - [JSON representation](#SparkStatistics.SCHEMA_REPRESENTATION)
  - [LoggingInfo](#LoggingInfo)
      - [JSON representation](#LoggingInfo.SCHEMA_REPRESENTATION)
  - [MaterializedViewStatistics](#MaterializedViewStatistics)
      - [JSON representation](#MaterializedViewStatistics.SCHEMA_REPRESENTATION)
  - [MaterializedView](#MaterializedView)
      - [JSON representation](#MaterializedView.SCHEMA_REPRESENTATION)
  - [RejectedReason](#RejectedReason)
  - [MetadataCacheStatistics](#MetadataCacheStatistics)
      - [JSON representation](#MetadataCacheStatistics.SCHEMA_REPRESENTATION)
  - [TableMetadataCacheUsage](#TableMetadataCacheUsage)
      - [JSON representation](#TableMetadataCacheUsage.SCHEMA_REPRESENTATION)
  - [UnusedReason](#UnusedReason)
  - [JobStatistics3](#JobStatistics3)
      - [JSON representation](#JobStatistics3.SCHEMA_REPRESENTATION)
  - [JobStatistics4](#JobStatistics4)
      - [JSON representation](#JobStatistics4.SCHEMA_REPRESENTATION)
  - [CopyJobStatistics](#CopyJobStatistics)
      - [JSON representation](#CopyJobStatistics.SCHEMA_REPRESENTATION)
  - [ScriptStatistics](#ScriptStatistics)
      - [JSON representation](#ScriptStatistics.SCHEMA_REPRESENTATION)
  - [EvaluationKind](#EvaluationKind)
  - [ScriptStackFrame](#ScriptStackFrame)
      - [JSON representation](#ScriptStackFrame.SCHEMA_REPRESENTATION)
  - [RowLevelSecurityStatistics](#RowLevelSecurityStatistics)
      - [JSON representation](#RowLevelSecurityStatistics.SCHEMA_REPRESENTATION)
  - [DataMaskingStatistics](#DataMaskingStatistics)
      - [JSON representation](#DataMaskingStatistics.SCHEMA_REPRESENTATION)
  - [TransactionInfo](#TransactionInfo)
      - [JSON representation](#TransactionInfo.SCHEMA_REPRESENTATION)
  - [ReservationEdition](#ReservationEdition)
  - [JobStatus](#JobStatus)
      - [JSON representation](#JobStatus.SCHEMA_REPRESENTATION)

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
  &quot;kind&quot;: string,
  &quot;etag&quot;: string,
  &quot;id&quot;: string,
  &quot;selfLink&quot;: string,
  &quot;user_email&quot;: string,
  &quot;configuration&quot;: {
    object (JobConfiguration)
  },
  &quot;jobReference&quot;: {
    object (JobReference)
  },
  &quot;statistics&quot;: {
    object (JobStatistics)
  },
  &quot;status&quot;: {
    object (JobStatus)
  },
  &quot;principal_subject&quot;: string,
  &quot;jobCreationReason&quot;: {
    object (JobCreationReason)
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  kind  `

`  string  `

Output only. The type of the resource.

`  etag  `

`  string  `

Output only. A hash of this resource.

`  id  `

`  string  `

Output only. Opaque ID field of the job.

`  selfLink  `

`  string  `

Output only. A URL that can be used to access the resource again.

`  user_email  `

`  string  `

Output only. Email address of the user who ran the job.

`  configuration  `

`  object ( JobConfiguration  ` )

Required. Describes the job configuration.

`  jobReference  `

`  object ( JobReference  ` )

Optional. Reference describing the unique-per-user name of the job.

`  statistics  `

`  object ( JobStatistics  ` )

Output only. Information about the job, including starting time and ending time of the job.

`  status  `

`  object ( JobStatus  ` )

Output only. The status of this job. Examine this value when polling an asynchronous job to see if the job is complete.

`  principal_subject  `

`  string  `

Output only. \[Full-projection-only\] String representation of identity of requesting party. Populated for both first- and third-party identities. Only present for APIs that support third-party identities.

`  jobCreationReason  `

`  object ( JobCreationReason  ` )

Output only. The reason why a Job was created.

## JobConfiguration

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
  &quot;jobType&quot;: string,
  &quot;query&quot;: {
    object (JobConfigurationQuery)
  },
  &quot;load&quot;: {
    object (JobConfigurationLoad)
  },
  &quot;copy&quot;: {
    object (JobConfigurationTableCopy)
  },
  &quot;extract&quot;: {
    object (JobConfigurationExtract)
  },
  &quot;dryRun&quot;: boolean,
  &quot;jobTimeoutMs&quot;: string,
  &quot;labels&quot;: {
    string: string,
    ...
  },
  &quot;reservation&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  jobType  `

`  string  `

Output only. The type of the job. Can be QUERY, LOAD, EXTRACT, COPY or UNKNOWN.

`  query  `

`  object ( JobConfigurationQuery  ` )

\[Pick one\] Configures a query job.

`  load  `

`  object ( JobConfigurationLoad  ` )

\[Pick one\] Configures a load job.

`  copy  `

`  object ( JobConfigurationTableCopy  ` )

\[Pick one\] Copies a table.

`  extract  `

`  object ( JobConfigurationExtract  ` )

\[Pick one\] Configures an extract job.

`  dryRun  `

`  boolean  `

Optional. If set, don't actually run this job. A valid query will return a mostly empty response with some processing statistics, while an invalid query will return the same error it would if it wasn't a dry run. Behavior of non-query jobs is undefined.

`  jobTimeoutMs  `

`  string ( Int64Value format)  `

Optional. Job timeout in milliseconds relative to the job creation time. If this time limit is exceeded, BigQuery attempts to stop the job, but might not always succeed in canceling it before the job completes. For example, a job that takes more than 60 seconds to complete has a better chance of being stopped than a job that takes 10 seconds to complete.

`  labels  `

`  map (key: string, value: string)  `

The labels associated with this job. You can use these to organize and group your jobs. Label keys and values can be no longer than 63 characters, can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. Label values are optional. Label keys must start with a letter and each label in the list must have a different key.

`  reservation  `

`  string  `

Optional. The reservation that job would use. User can specify a reservation to execute the job. If reservation is not set, reservation is determined based on the rules defined by the reservation assignments. The expected format is `  projects/{project}/locations/{location}/reservations/{reservation}  ` .

## JobConfigurationQuery

JobConfigurationQuery configures a BigQuery query job.

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
  &quot;query&quot;: string,
  &quot;destinationTable&quot;: {
    object (TableReference)
  },
  &quot;tableDefinitions&quot;: {
    string: {
      object (ExternalDataConfiguration)
    },
    ...
  },
  &quot;userDefinedFunctionResources&quot;: [
    {
      object (UserDefinedFunctionResource)
    }
  ],
  &quot;createDisposition&quot;: string,
  &quot;writeDisposition&quot;: string,
  &quot;defaultDataset&quot;: {
    object (DatasetReference)
  },
  &quot;priority&quot;: string,
  &quot;preserveNulls&quot;: boolean,
  &quot;allowLargeResults&quot;: boolean,
  &quot;useQueryCache&quot;: boolean,
  &quot;flattenResults&quot;: boolean,
  &quot;maximumBillingTier&quot;: integer,
  &quot;maximumBytesBilled&quot;: string,
  &quot;useLegacySql&quot;: boolean,
  &quot;parameterMode&quot;: string,
  &quot;queryParameters&quot;: [
    {
      object (QueryParameter)
    }
  ],
  &quot;schemaUpdateOptions&quot;: [
    string
  ],
  &quot;timePartitioning&quot;: {
    object (TimePartitioning)
  },
  &quot;rangePartitioning&quot;: {
    object (RangePartitioning)
  },
  &quot;clustering&quot;: {
    object (Clustering)
  },
  &quot;destinationEncryptionConfiguration&quot;: {
    object (EncryptionConfiguration)
  },
  &quot;scriptOptions&quot;: {
    object (ScriptOptions)
  },
  &quot;connectionProperties&quot;: [
    {
      object (ConnectionProperty)
    }
  ],
  &quot;createSession&quot;: boolean,
  &quot;systemVariables&quot;: {
    object (SystemVariables)
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  query  `

`  string  `

\[Required\] SQL query text to execute. The useLegacySql field can be used to indicate whether the query uses legacy SQL or GoogleSQL.

`  destinationTable  `

`  object ( TableReference  ` )

Optional. Describes the table where the query results should be stored. This property must be set for large results that exceed the maximum response size. For queries that produce anonymous (cached) results, this field will be populated by BigQuery.

`  tableDefinitions  `

`  map (key: string, value: object ( ExternalDataConfiguration  ` ))

Optional. You can specify external table definitions, which operate as ephemeral tables that can be queried. These definitions are configured using a JSON map, where the string key represents the table identifier, and the value is the corresponding external data configuration object.

`  userDefinedFunctionResources[]  `

`  object ( UserDefinedFunctionResource  ` )

Describes user-defined function resources used in the query.

`  createDisposition  `

`  string  `

Optional. Specifies whether the job is allowed to create new tables. The following values are supported:

  - CREATE\_IF\_NEEDED: If the table does not exist, BigQuery creates the table.
  - CREATE\_NEVER: The table must already exist. If it does not, a 'notFound' error is returned in the job result.

The default value is CREATE\_IF\_NEEDED. Creation, truncation and append actions occur as one atomic update upon job completion.

`  writeDisposition  `

`  string  `

Optional. Specifies the action that occurs if the destination table already exists. The following values are supported:

  - WRITE\_TRUNCATE: If the table already exists, BigQuery overwrites the data, removes the constraints, and uses the schema from the query result.
  - WRITE\_TRUNCATE\_DATA: If the table already exists, BigQuery overwrites the data, but keeps the constraints and schema of the existing table.
  - WRITE\_APPEND: If the table already exists, BigQuery appends the data to the table.
  - WRITE\_EMPTY: If the table already exists and contains data, a 'duplicate' error is returned in the job result.

The default value is WRITE\_EMPTY. Each action is atomic and only occurs if BigQuery is able to complete the job successfully. Creation, truncation and append actions occur as one atomic update upon job completion.

`  defaultDataset  `

`  object ( DatasetReference  ` )

Optional. Specifies the default dataset to use for unqualified table names in the query. This setting does not alter behavior of unqualified dataset names. Setting the system variable `  @@dataset_id  ` achieves the same behavior. See <https://cloud.google.com/bigquery/docs/reference/system-variables> for more information on system variables.

`  priority  `

`  string  `

Optional. Specifies a priority for the query. Possible values include INTERACTIVE and BATCH. The default value is INTERACTIVE.

`  preserveNulls  `

`  boolean  `

\[Deprecated\] This property is deprecated.

`  allowLargeResults  `

`  boolean  `

Optional. If true and query uses legacy SQL dialect, allows the query to produce arbitrarily large result tables at a slight cost in performance. Requires destinationTable to be set. For GoogleSQL queries, this flag is ignored and large results are always allowed. However, you must still set destinationTable when result size exceeds the allowed maximum response size.

`  useQueryCache  `

`  boolean  `

Optional. Whether to look for the result in the query cache. The query cache is a best-effort cache that will be flushed whenever tables in the query are modified. Moreover, the query cache is only available when a query does not have a destination table specified. The default value is true.

`  flattenResults  `

`  boolean  `

Optional. If true and query uses legacy SQL dialect, flattens all nested and repeated fields in the query results. allowLargeResults must be true if this is set to false. For GoogleSQL queries, this flag is ignored and results are never flattened.

`  maximumBillingTier  `

`  integer  `

Optional. \[Deprecated\] Maximum billing tier allowed for this query. The billing tier controls the amount of compute resources allotted to the query, and multiplies the on-demand cost of the query accordingly. A query that runs within its allotted resources will succeed and indicate its billing tier in statistics.query.billingTier, but if the query exceeds its allotted resources, it will fail with billingTierLimitExceeded. WARNING: The billed byte amount can be multiplied by an amount up to this number\! Most users should not need to alter this setting, and we recommend that you avoid introducing new uses of it.

`  maximumBytesBilled  `

`  string ( Int64Value format)  `

Limits the bytes billed for this job. Queries that will have bytes billed beyond this limit will fail (without incurring a charge). If unspecified, this will be set to your project default.

`  useLegacySql  `

`  boolean  `

Optional. Specifies whether to use BigQuery's legacy SQL dialect for this query. The default value is true. If set to false, the query uses BigQuery's [GoogleSQL](https://docs.cloud.google.com/bigquery/docs/introduction-sql) .

When useLegacySql is set to false, the value of flattenResults is ignored; query will be run as if flattenResults is false.

`  parameterMode  `

`  string  `

GoogleSQL only. Set to POSITIONAL to use positional (?) query parameters or to NAMED to use named (@myparam) query parameters in this query.

`  queryParameters[]  `

`  object ( QueryParameter  ` )

jobs.query parameters for GoogleSQL queries.

`  schemaUpdateOptions[]  `

`  string  `

Allows the schema of the destination table to be updated as a side effect of the query job. Schema update options are supported in three cases: when writeDisposition is WRITE\_APPEND; when writeDisposition is WRITE\_TRUNCATE\_DATA; when writeDisposition is WRITE\_TRUNCATE and the destination table is a partition of a table, specified by partition decorators. For normal tables, WRITE\_TRUNCATE will always overwrite the schema. One or more of the following values are specified:

  - ALLOW\_FIELD\_ADDITION: allow adding a nullable field to the schema.
  - ALLOW\_FIELD\_RELAXATION: allow relaxing a required field in the original schema to nullable.

`  timePartitioning  `

`  object ( TimePartitioning  ` )

Time-based partitioning specification for the destination table. Only one of timePartitioning and rangePartitioning should be specified.

`  rangePartitioning  `

`  object ( RangePartitioning  ` )

Range partitioning specification for the destination table. Only one of timePartitioning and rangePartitioning should be specified.

`  clustering  `

`  object ( Clustering  ` )

Clustering specification for the destination table.

`  destinationEncryptionConfiguration  `

`  object ( EncryptionConfiguration  ` )

Custom encryption configuration (e.g., Cloud KMS keys)

`  scriptOptions  `

`  object ( ScriptOptions  ` )

Options controlling the execution of scripts.

`  connectionProperties[]  `

`  object ( ConnectionProperty  ` )

Connection properties which can modify the query behavior.

`  createSession  `

`  boolean  `

If this property is true, the job creates a new session using a randomly generated sessionId. To continue using a created session with subsequent queries, pass the existing session identifier as a `  ConnectionProperty  ` value. The session identifier is returned as part of the `  SessionInfo  ` message within the query statistics.

The new session's location will be set to `  Job.JobReference.location  ` if it is present, otherwise it's set to the default location based on existing routing logic.

`  systemVariables  `

`  object ( SystemVariables  ` )

Output only. System variables for GoogleSQL queries. A system variable is output if the variable is settable and its value differs from the system default. "@@" prefix is not included in the name of the System variables.

## SystemVariables

System variables given to a query.

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
  &quot;types&quot;: {
    string: {
      object (StandardSqlDataType)
    },
    ...
  },
  &quot;values&quot;: {
    object
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  types  `

`  map (key: string, value: object ( StandardSqlDataType  ` ))

Output only. Data type for each system variable.

`  values  `

`  object ( Struct  ` format)

Output only. Value for each system variable.

## ScriptOptions

Options related to script execution.

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
  &quot;statementTimeoutMs&quot;: string,
  &quot;statementByteBudget&quot;: string,
  &quot;keyResultStatement&quot;: enum (KeyResultStatementKind)
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  statementTimeoutMs  `

`  string ( Int64Value format)  `

Timeout period for each statement in a script.

`  statementByteBudget  `

`  string ( Int64Value format)  `

Limit on the number of bytes billed per statement. Exceeding this budget results in an error.

`  keyResultStatement  `

`  enum ( KeyResultStatementKind  ` )

Determines which statement in the script represents the "key result", used to populate the schema and query results of the script job. Default is LAST.

## KeyResultStatementKind

KeyResultStatementKind controls how the key result is determined.

Enums

`  KEY_RESULT_STATEMENT_KIND_UNSPECIFIED  `

Default value.

`  LAST  `

The last result determines the key result.

`  FIRST_SELECT  `

The first SELECT statement determines the key result.

## JobConfigurationLoad

JobConfigurationLoad contains the configuration properties for loading data into a destination table.

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
  &quot;sourceUris&quot;: [
    string
  ],
  &quot;fileSetSpecType&quot;: enum (FileSetSpecType),
  &quot;schema&quot;: {
    object (TableSchema)
  },
  &quot;destinationTable&quot;: {
    object (TableReference)
  },
  &quot;destinationTableProperties&quot;: {
    object (DestinationTableProperties)
  },
  &quot;createDisposition&quot;: string,
  &quot;writeDisposition&quot;: string,
  &quot;nullMarker&quot;: string,
  &quot;fieldDelimiter&quot;: string,
  &quot;skipLeadingRows&quot;: integer,
  &quot;encoding&quot;: string,
  &quot;quote&quot;: string,
  &quot;maxBadRecords&quot;: integer,
  &quot;schemaInlineFormat&quot;: string,
  &quot;schemaInline&quot;: string,
  &quot;allowQuotedNewlines&quot;: boolean,
  &quot;sourceFormat&quot;: string,
  &quot;allowJaggedRows&quot;: boolean,
  &quot;ignoreUnknownValues&quot;: boolean,
  &quot;projectionFields&quot;: [
    string
  ],
  &quot;autodetect&quot;: boolean,
  &quot;schemaUpdateOptions&quot;: [
    string
  ],
  &quot;timePartitioning&quot;: {
    object (TimePartitioning)
  },
  &quot;rangePartitioning&quot;: {
    object (RangePartitioning)
  },
  &quot;clustering&quot;: {
    object (Clustering)
  },
  &quot;destinationEncryptionConfiguration&quot;: {
    object (EncryptionConfiguration)
  },
  &quot;useAvroLogicalTypes&quot;: boolean,
  &quot;referenceFileSchemaUri&quot;: string,
  &quot;hivePartitioningOptions&quot;: {
    object (HivePartitioningOptions)
  },
  &quot;decimalTargetTypes&quot;: [
    enum (DecimalTargetType)
  ],
  &quot;jsonExtension&quot;: enum (JsonExtension),
  &quot;parquetOptions&quot;: {
    object (ParquetOptions)
  },
  &quot;preserveAsciiControlCharacters&quot;: boolean,
  &quot;columnNameCharacterMap&quot;: enum (ColumnNameCharacterMap),
  &quot;copyFilesOnly&quot;: boolean,
  &quot;timeZone&quot;: string,
  &quot;nullMarkers&quot;: [
    string
  ],
  &quot;sourceColumnMatch&quot;: enum (SourceColumnMatch),
  &quot;dateFormat&quot;: string,
  &quot;datetimeFormat&quot;: string,
  &quot;timeFormat&quot;: string,
  &quot;timestampFormat&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  sourceUris[]  `

`  string  `

\[Required\] The fully-qualified URIs that point to your data in Google Cloud. For Google Cloud Storage URIs: Each URI can contain one '\*' wildcard character and it must come after the 'bucket' name. Size limits related to load jobs apply to external data sources. For Google Cloud Bigtable URIs: Exactly one URI can be specified and it has be a fully specified and valid HTTPS URL for a Google Cloud Bigtable table. For Google Cloud Datastore backups: Exactly one URI can be specified. Also, the '\*' wildcard character is not allowed.

`  fileSetSpecType  `

`  enum ( FileSetSpecType  ` )

Optional. Specifies how source URIs are interpreted for constructing the file set to load. By default, source URIs are expanded against the underlying storage. You can also specify manifest files to control how the file set is constructed. This option is only applicable to object storage systems.

`  schema  `

`  object ( TableSchema  ` )

Optional. The schema for the destination table. The schema can be omitted if the destination table already exists, or if you're loading data from Google Cloud Datastore.

`  destinationTable  `

`  object ( TableReference  ` )

\[Required\] The destination table to load the data into.

`  destinationTableProperties  `

`  object ( DestinationTableProperties  ` )

Optional. \[Experimental\] Properties with which to create the destination table if it is new.

`  createDisposition  `

`  string  `

Optional. Specifies whether the job is allowed to create new tables. The following values are supported:

  - CREATE\_IF\_NEEDED: If the table does not exist, BigQuery creates the table.
  - CREATE\_NEVER: The table must already exist. If it does not, a 'notFound' error is returned in the job result. The default value is CREATE\_IF\_NEEDED. Creation, truncation and append actions occur as one atomic update upon job completion.

`  writeDisposition  `

`  string  `

Optional. Specifies the action that occurs if the destination table already exists. The following values are supported:

  - WRITE\_TRUNCATE: If the table already exists, BigQuery overwrites the data, removes the constraints and uses the schema from the load job.
  - WRITE\_TRUNCATE\_DATA: If the table already exists, BigQuery overwrites the data, but keeps the constraints and schema of the existing table.
  - WRITE\_APPEND: If the table already exists, BigQuery appends the data to the table.
  - WRITE\_EMPTY: If the table already exists and contains data, a 'duplicate' error is returned in the job result.

The default value is WRITE\_APPEND. Each action is atomic and only occurs if BigQuery is able to complete the job successfully. Creation, truncation and append actions occur as one atomic update upon job completion.

`  nullMarker  `

`  string  `

Optional. Specifies a string that represents a null value in a CSV file. For example, if you specify "\\N", BigQuery interprets "\\N" as a null value when loading a CSV file. The default value is the empty string. If you set this property to a custom value, BigQuery throws an error if an empty string is present for all data types except for STRING and BYTE. For STRING and BYTE columns, BigQuery interprets the empty string as an empty value.

`  fieldDelimiter  `

`  string  `

Optional. The separator character for fields in a CSV file. The separator is interpreted as a single byte. For files encoded in ISO-8859-1, any single character can be used as a separator. For files encoded in UTF-8, characters represented in decimal range 1-127 (U+0001-U+007F) can be used without any modification. UTF-8 characters encoded with multiple bytes (i.e. U+0080 and above) will have only the first byte used for separating fields. The remaining bytes will be treated as a part of the field. BigQuery also supports the escape sequence "\\t" (U+0009) to specify a tab separator. The default value is comma (",", U+002C).

`  skipLeadingRows  `

`  integer  `

Optional. The number of rows at the top of a CSV file that BigQuery will skip when loading the data. The default value is 0. This property is useful if you have header rows in the file that should be skipped. When autodetect is on, the behavior is the following:

  - skipLeadingRows unspecified - Autodetect tries to detect headers in the first row. If they are not detected, the row is read as data. Otherwise data is read starting from the second row.
  - skipLeadingRows is 0 - Instructs autodetect that there are no headers and data should be read starting from the first row.
  - skipLeadingRows = N \> 0 - Autodetect skips N-1 rows and tries to detect headers in row N. If headers are not detected, row N is just skipped. Otherwise row N is used to extract column names for the detected schema.

`  encoding  `

`  string  `

Optional. The character encoding of the data. The supported values are UTF-8, ISO-8859-1, UTF-16BE, UTF-16LE, UTF-32BE, and UTF-32LE. The default value is UTF-8. BigQuery decodes the data after the raw, binary data has been split using the values of the `  quote  ` and `  fieldDelimiter  ` properties.

If you don't specify an encoding, or if you specify a UTF-8 encoding when the CSV file is not UTF-8 encoded, BigQuery attempts to convert the data to UTF-8. Generally, your data loads successfully, but it may not match byte-for-byte what you expect. To avoid this, specify the correct encoding by using the `  --encoding  ` flag.

If BigQuery can't convert a character other than the ASCII `  0  ` character, BigQuery converts the character to the standard Unicode replacement character: �.

`  quote  `

`  string  `

Optional. The value that is used to quote data sections in a CSV file. BigQuery converts the string to ISO-8859-1 encoding, and then uses the first byte of the encoded string to split the data in its raw, binary state. The default value is a double-quote ('"'). If your data does not contain quoted sections, set the property value to an empty string. If your data contains quoted newline characters, you must also set the allowQuotedNewlines property to true. To include the specific quote character within a quoted value, precede it with an additional matching quote character. For example, if you want to escape the default character ' " ', use ' "" '. @default "

`  maxBadRecords  `

`  integer  `

Optional. The maximum number of bad records that BigQuery can ignore when running the job. If the number of bad records exceeds this value, an invalid error is returned in the job result. The default value is 0, which requires that all records are valid. This is only supported for CSV and NEWLINE\_DELIMITED\_JSON file formats.

`  schemaInlineFormat  `

`  string  `

\[Deprecated\] The format of the schemaInline property.

`  schemaInline  `

`  string  `

\[Deprecated\] The inline schema. For CSV schemas, specify as "Field1:Type1\[,Field2:Type2\]\*". For example, "foo:STRING, bar:INTEGER, baz:FLOAT".

`  allowQuotedNewlines  `

`  boolean  `

Indicates if BigQuery should allow quoted data sections that contain newline characters in a CSV file. The default value is false.

`  sourceFormat  `

`  string  `

Optional. The format of the data files. For CSV files, specify "CSV". For datastore backups, specify "DATASTORE\_BACKUP". For newline-delimited JSON, specify "NEWLINE\_DELIMITED\_JSON". For Avro, specify "AVRO". For parquet, specify "PARQUET". For orc, specify "ORC". The default value is CSV.

`  allowJaggedRows  `

`  boolean  `

Optional. Accept rows that are missing trailing optional columns. The missing values are treated as nulls. If false, records with missing trailing columns are treated as bad records, and if there are too many bad records, an invalid error is returned in the job result. The default value is false. Only applicable to CSV, ignored for other formats.

`  ignoreUnknownValues  `

`  boolean  `

Optional. Indicates if BigQuery should allow extra values that are not represented in the table schema. If true, the extra values are ignored. If false, records with extra columns are treated as bad records, and if there are too many bad records, an invalid error is returned in the job result. The default value is false. The sourceFormat property determines what BigQuery treats as an extra value: CSV: Trailing columns JSON: Named values that don't match any column names in the table schema Avro, Parquet, ORC: Fields in the file schema that don't exist in the table schema.

`  projectionFields[]  `

`  string  `

If sourceFormat is set to "DATASTORE\_BACKUP", indicates which entity properties to load into BigQuery from a Cloud Datastore backup. Property names are case sensitive and must be top-level properties. If no properties are specified, BigQuery loads all properties. If any named property isn't found in the Cloud Datastore backup, an invalid error is returned in the job result.

`  autodetect  `

`  boolean  `

Optional. Indicates if we should automatically infer the options and schema for CSV and JSON sources.

`  schemaUpdateOptions[]  `

`  string  `

Allows the schema of the destination table to be updated as a side effect of the load job if a schema is autodetected or supplied in the job configuration. Schema update options are supported in three cases: when writeDisposition is WRITE\_APPEND; when writeDisposition is WRITE\_TRUNCATE\_DATA; when writeDisposition is WRITE\_TRUNCATE and the destination table is a partition of a table, specified by partition decorators. For normal tables, WRITE\_TRUNCATE will always overwrite the schema. One or more of the following values are specified:

  - ALLOW\_FIELD\_ADDITION: allow adding a nullable field to the schema.
  - ALLOW\_FIELD\_RELAXATION: allow relaxing a required field in the original schema to nullable.

`  timePartitioning  `

`  object ( TimePartitioning  ` )

Time-based partitioning specification for the destination table. Only one of timePartitioning and rangePartitioning should be specified.

`  rangePartitioning  `

`  object ( RangePartitioning  ` )

Range partitioning specification for the destination table. Only one of timePartitioning and rangePartitioning should be specified.

`  clustering  `

`  object ( Clustering  ` )

Clustering specification for the destination table.

`  destinationEncryptionConfiguration  `

`  object ( EncryptionConfiguration  ` )

Custom encryption configuration (e.g., Cloud KMS keys)

`  useAvroLogicalTypes  `

`  boolean  `

Optional. If sourceFormat is set to "AVRO", indicates whether to interpret logical types as the corresponding BigQuery data type (for example, TIMESTAMP), instead of using the raw type (for example, INTEGER).

`  referenceFileSchemaUri  `

`  string  `

Optional. The user can provide a reference file with the reader schema. This file is only loaded if it is part of source URIs, but is not loaded otherwise. It is enabled for the following formats: AVRO, PARQUET, ORC.

`  hivePartitioningOptions  `

`  object ( HivePartitioningOptions  ` )

Optional. When set, configures hive partitioning support. Not all storage formats support hive partitioning -- requesting hive partitioning on an unsupported format will lead to an error, as will providing an invalid specification.

`  decimalTargetTypes[]  `

`  enum ( DecimalTargetType  ` )

Defines the list of possible SQL data types to which the source decimal values are converted. This list and the precision and the scale parameters of the decimal field determine the target type. In the order of NUMERIC, BIGNUMERIC, and STRING, a type is picked if it is in the specified list and if it supports the precision and the scale. STRING supports all precision and scale values. If none of the listed types supports the precision and the scale, the type supporting the widest range in the specified list is picked, and if a value exceeds the supported range when reading the data, an error will be thrown.

Example: Suppose the value of this field is \["NUMERIC", "BIGNUMERIC"\]. If (precision,scale) is:

  - (38,9) -\> NUMERIC;
  - (39,9) -\> BIGNUMERIC (NUMERIC cannot hold 30 integer digits);
  - (38,10) -\> BIGNUMERIC (NUMERIC cannot hold 10 fractional digits);
  - (76,38) -\> BIGNUMERIC;
  - (77,38) -\> BIGNUMERIC (error if value exceeds supported range).

This field cannot contain duplicate types. The order of the types in this field is ignored. For example, \["BIGNUMERIC", "NUMERIC"\] is the same as \["NUMERIC", "BIGNUMERIC"\] and NUMERIC always takes precedence over BIGNUMERIC.

Defaults to \["NUMERIC", "STRING"\] for ORC and \["NUMERIC"\] for the other file formats.

`  jsonExtension  `

`  enum ( JsonExtension  ` )

Optional. Load option to be used together with sourceFormat newline-delimited JSON to indicate that a variant of JSON is being loaded. To load newline-delimited GeoJSON, specify GEOJSON (and sourceFormat must be set to NEWLINE\_DELIMITED\_JSON).

`  parquetOptions  `

`  object ( ParquetOptions  ` )

Optional. Additional properties to set if sourceFormat is set to PARQUET.

`  preserveAsciiControlCharacters  `

`  boolean  `

Optional. When sourceFormat is set to "CSV", this indicates whether the embedded ASCII control characters (the first 32 characters in the ASCII-table, from '\\x00' to '\\x1F') are preserved.

`  columnNameCharacterMap  `

`  enum ( ColumnNameCharacterMap  ` )

Optional. Character map supported for column names in CSV/Parquet loads. Defaults to STRICT and can be overridden by Project Config Service. Using this option with unsupporting load formats will result in an error.

`  copyFilesOnly  `

`  boolean  `

Optional. \[Experimental\] Configures the load job to copy files directly to the destination BigLake managed table, bypassing file content reading and rewriting.

Copying files only is supported when all the following are true:

  - `  sourceUris  ` are located in the same Cloud Storage location as the destination table's `  storageUri  ` location.
  - `  sourceFormat  ` is `  PARQUET  ` .
  - `  destinationTable  ` is an existing BigLake managed table. The table's schema does not have flexible column names. The table's columns do not have type parameters other than precision and scale.
  - No options other than the above are specified.

`  timeZone  `

`  string  `

Optional. Default time zone that will apply when parsing timestamp values that have no specific time zone.

`  nullMarkers[]  `

`  string  `

Optional. A list of strings represented as SQL NULL value in a CSV file.

nullMarker and nullMarkers can't be set at the same time. If nullMarker is set, nullMarkers has to be not set. If nullMarkers is set, nullMarker has to be not set. If both nullMarker and nullMarkers are set at the same time, a user error would be thrown. Any strings listed in nullMarkers, including empty string would be interpreted as SQL NULL. This applies to all column types.

`  sourceColumnMatch  `

`  enum ( SourceColumnMatch  ` )

Optional. Controls the strategy used to match loaded columns to the schema. If not set, a sensible default is chosen based on how the schema is provided. If autodetect is used, then columns are matched by name. Otherwise, columns are matched by position. This is done to keep the behavior backward-compatible.

`  dateFormat  `

`  string  `

Optional. Date format used for parsing DATE values.

`  datetimeFormat  `

`  string  `

Optional. Date format used for parsing DATETIME values.

`  timeFormat  `

`  string  `

Optional. Date format used for parsing TIME values.

`  timestampFormat  `

`  string  `

Optional. Date format used for parsing TIMESTAMP values.

## DestinationTableProperties

Properties for the destination table.

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
  &quot;friendlyName&quot;: string,
  &quot;description&quot;: string,
  &quot;labels&quot;: {
    string: string,
    ...
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  friendlyName  `

`  string  `

Optional. Friendly name for the destination table. If the table already exists, it should be same as the existing friendly name.

`  description  `

`  string  `

Optional. The description for the destination table. This will only be used if the destination table is newly created. If the table already exists and a value different than the current description is provided, the job will fail.

`  labels  `

`  map (key: string, value: string)  `

Optional. The labels associated with this table. You can use these to organize and group your tables. This will only be used if the destination table is newly created. If the table already exists and labels are different than the current labels are provided, the job will fail.

## ColumnNameCharacterMap

Indicates the character map used for column names.

Enums

`  COLUMN_NAME_CHARACTER_MAP_UNSPECIFIED  `

Unspecified column name character map.

`  STRICT  `

Support flexible column name and reject invalid column names.

`  V1  `

Support alphanumeric + underscore characters and names must start with a letter or underscore. Invalid column names will be normalized.

`  V2  `

Support flexible column name. Invalid column names will be normalized.

## SourceColumnMatch

Indicates the strategy used to match loaded columns to the schema.

Enums

`  SOURCE_COLUMN_MATCH_UNSPECIFIED  `

Uses sensible defaults based on how the schema is provided. If autodetect is used, then columns are matched by name. Otherwise, columns are matched by position. This is done to keep the behavior backward-compatible.

`  POSITION  `

Matches by position. This assumes that the columns are ordered the same way as the schema.

`  NAME  `

Matches by name. This reads the header row as column names and reorders columns to match the field names in the schema.

## JobConfigurationTableCopy

JobConfigurationTableCopy configures a job that copies data from one table to another. For more information on copying tables, see [Copy a table](https://cloud.google.com/bigquery/docs/managing-tables#copy-table) .

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
  &quot;sourceTable&quot;: {
    object (TableReference)
  },
  &quot;sourceTables&quot;: [
    {
      object (TableReference)
    }
  ],
  &quot;destinationTable&quot;: {
    object (TableReference)
  },
  &quot;createDisposition&quot;: string,
  &quot;writeDisposition&quot;: string,
  &quot;destinationEncryptionConfiguration&quot;: {
    object (EncryptionConfiguration)
  },
  &quot;operationType&quot;: enum (OperationType),
  &quot;destinationExpirationTime&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  sourceTable  `

`  object ( TableReference  ` )

\[Pick one\] Source table to copy.

`  sourceTables[]  `

`  object ( TableReference  ` )

\[Pick one\] Source tables to copy.

`  destinationTable  `

`  object ( TableReference  ` )

\[Required\] The destination table.

`  createDisposition  `

`  string  `

Optional. Specifies whether the job is allowed to create new tables. The following values are supported:

  - CREATE\_IF\_NEEDED: If the table does not exist, BigQuery creates the table.
  - CREATE\_NEVER: The table must already exist. If it does not, a 'notFound' error is returned in the job result.

The default value is CREATE\_IF\_NEEDED. Creation, truncation and append actions occur as one atomic update upon job completion.

`  writeDisposition  `

`  string  `

Optional. Specifies the action that occurs if the destination table already exists. The following values are supported:

  - WRITE\_TRUNCATE: If the table already exists, BigQuery overwrites the table data and uses the schema and table constraints from the source table.
  - WRITE\_APPEND: If the table already exists, BigQuery appends the data to the table.
  - WRITE\_EMPTY: If the table already exists and contains data, a 'duplicate' error is returned in the job result.

The default value is WRITE\_EMPTY. Each action is atomic and only occurs if BigQuery is able to complete the job successfully. Creation, truncation and append actions occur as one atomic update upon job completion.

`  destinationEncryptionConfiguration  `

`  object ( EncryptionConfiguration  ` )

Custom encryption configuration (e.g., Cloud KMS keys).

`  operationType  `

`  enum ( OperationType  ` )

Optional. Supported operation types in table copy job.

`  destinationExpirationTime  `

`  string ( Timestamp  ` format)

Optional. The time when the destination table expires. Expired tables will be deleted and their storage reclaimed.

## OperationType

Indicates different operation types supported in table copy job.

Enums

`  OPERATION_TYPE_UNSPECIFIED  `

Unspecified operation type.

`  COPY  `

The source and destination table have the same table type.

`  SNAPSHOT  `

The source table type is TABLE and the destination table type is SNAPSHOT.

`  RESTORE  `

The source table type is SNAPSHOT and the destination table type is TABLE.

`  CLONE  `

The source and destination table have the same table type, but only bill for unique data.

## JobConfigurationExtract

JobConfigurationExtract configures a job that exports data from a BigQuery table into Google Cloud Storage.

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
  &quot;destinationUri&quot;: string,
  &quot;destinationUris&quot;: [
    string
  ],
  &quot;printHeader&quot;: boolean,
  &quot;fieldDelimiter&quot;: string,
  &quot;destinationFormat&quot;: string,
  &quot;compression&quot;: string,
  &quot;useAvroLogicalTypes&quot;: boolean,
  &quot;modelExtractOptions&quot;: {
    object (ModelExtractOptions)
  },

  // Union field source can be only one of the following:
  &quot;sourceTable&quot;: {
    object (TableReference)
  },
  &quot;sourceModel&quot;: {
    object (ModelReference)
  }
  // End of list of possible types for union field source.
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  destinationUri  `

`  string  `

\[Pick one\] DEPRECATED: Use destinationUris instead, passing only one URI as necessary. The fully-qualified Google Cloud Storage URI where the extracted table should be written.

`  destinationUris[]  `

`  string  `

\[Pick one\] A list of fully-qualified Google Cloud Storage URIs where the extracted table should be written.

`  printHeader  `

`  boolean  `

Optional. Whether to print out a header row in the results. Default is true. Not applicable when extracting models.

`  fieldDelimiter  `

`  string  `

Optional. When extracting data in CSV format, this defines the delimiter to use between fields in the exported data. Default is ','. Not applicable when extracting models.

`  destinationFormat  `

`  string  `

Optional. The exported file format. Possible values include CSV, NEWLINE\_DELIMITED\_JSON, PARQUET, or AVRO for tables and ML\_TF\_SAVED\_MODEL or ML\_XGBOOST\_BOOSTER for models. The default value for tables is CSV. Tables with nested or repeated fields cannot be exported as CSV. The default value for models is ML\_TF\_SAVED\_MODEL.

`  compression  `

`  string  `

Optional. The compression type to use for exported files. Possible values include DEFLATE, GZIP, NONE, SNAPPY, and ZSTD. The default value is NONE. Not all compression formats are support for all file formats. DEFLATE is only supported for Avro. ZSTD is only supported for Parquet. Not applicable when extracting models.

`  useAvroLogicalTypes  `

`  boolean  `

Whether to use logical types when extracting to AVRO format. Not applicable when extracting models.

`  modelExtractOptions  `

`  object ( ModelExtractOptions  ` )

Optional. Model extract options only applicable when extracting models.

Union field `  source  ` . Required. Source reference for the export. `  source  ` can be only one of the following:

`  sourceTable  `

`  object ( TableReference  ` )

A reference to the table being exported.

`  sourceModel  `

`  object ( ModelReference  ` )

A reference to the model being exported.

## ModelExtractOptions

Options related to model extraction.

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
  &quot;trialId&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  trialId  `

`  string ( Int64Value format)  `

The 1-based ID of the trial to be exported from a hyperparameter tuning model. If not specified, the trial with id = [Model](https://cloud.google.com/bigquery/docs/reference/rest/v2/models#resource:-model) .defaultTrialId is exported. This field is ignored for models not trained with hyperparameter tuning.

## JobStatistics

Statistics for a single job execution.

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
  &quot;creationTime&quot;: string,
  &quot;startTime&quot;: string,
  &quot;endTime&quot;: string,
  &quot;totalBytesProcessed&quot;: string,
  &quot;completionRatio&quot;: number,
  &quot;quotaDeferments&quot;: [
    string
  ],
  &quot;query&quot;: {
    object (JobStatistics2)
  },
  &quot;load&quot;: {
    object (JobStatistics3)
  },
  &quot;extract&quot;: {
    object (JobStatistics4)
  },
  &quot;copy&quot;: {
    object (CopyJobStatistics)
  },
  &quot;totalSlotMs&quot;: string,
  &quot;reservationUsage&quot;: [
    {
      &quot;name&quot;: string,
      &quot;slotMs&quot;: string
    }
  ],
  &quot;reservation_id&quot;: string,
  &quot;numChildJobs&quot;: string,
  &quot;parentJobId&quot;: string,
  &quot;scriptStatistics&quot;: {
    object (ScriptStatistics)
  },
  &quot;rowLevelSecurityStatistics&quot;: {
    object (RowLevelSecurityStatistics)
  },
  &quot;dataMaskingStatistics&quot;: {
    object (DataMaskingStatistics)
  },
  &quot;transactionInfo&quot;: {
    object (TransactionInfo)
  },
  &quot;sessionInfo&quot;: {
    object (SessionInfo)
  },
  &quot;finalExecutionDurationMs&quot;: string,
  &quot;edition&quot;: enum (ReservationEdition)
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  creationTime  `

`  string ( int64 format)  `

Output only. Creation time of this job, in milliseconds since the epoch. This field will be present on all jobs.

`  startTime  `

`  string ( int64 format)  `

Output only. Start time of this job, in milliseconds since the epoch. This field will be present when the job transitions from the PENDING state to either RUNNING or DONE.

`  endTime  `

`  string ( int64 format)  `

Output only. End time of this job, in milliseconds since the epoch. This field will be present whenever a job is in the DONE state.

`  totalBytesProcessed  `

`  string ( Int64Value format)  `

Output only. Total bytes processed for the job.

`  completionRatio  `

`  number  `

Output only. \[TrustedTester\] Job progress (0.0 -\> 1.0) for LOAD and EXTRACT jobs.

`  quotaDeferments[]  `

`  string  `

Output only. Quotas which delayed this job's start time.

`  query  `

`  object ( JobStatistics2  ` )

Output only. Statistics for a query job.

`  load  `

`  object ( JobStatistics3  ` )

Output only. Statistics for a load job.

`  extract  `

`  object ( JobStatistics4  ` )

Output only. Statistics for an extract job.

`  copy  `

`  object ( CopyJobStatistics  ` )

Output only. Statistics for a copy job.

`  totalSlotMs  `

`  string ( Int64Value format)  `

Output only. Slot-milliseconds for the job.

`  reservationUsage[] (deprecated)  `

`  object  `

This item is deprecated\!

Output only. Job resource usage breakdown by reservation. This field reported misleading information and will no longer be populated.

`  reservationUsage[] (deprecated) .name  `

`  string  `

Reservation name or "unreserved" for on-demand resource usage and multi-statement queries.

`  reservationUsage[] (deprecated) .slotMs  `

`  string ( Int64Value format)  `

Total slot milliseconds used by the reservation for a particular job.

`  reservation_id  `

`  string  `

Output only. Name of the primary reservation assigned to this job. Note that this could be different than reservations reported in the reservation usage field if parent reservations were used to execute this job.

`  numChildJobs  `

`  string ( int64 format)  `

Output only. Number of child jobs executed.

`  parentJobId  `

`  string  `

Output only. If this is a child job, specifies the job ID of the parent.

`  scriptStatistics  `

`  object ( ScriptStatistics  ` )

Output only. If this a child job of a script, specifies information about the context of this job within the script.

`  rowLevelSecurityStatistics  `

`  object ( RowLevelSecurityStatistics  ` )

Output only. Statistics for row-level security. Present only for query and extract jobs.

`  dataMaskingStatistics  `

`  object ( DataMaskingStatistics  ` )

Output only. Statistics for data-masking. Present only for query and extract jobs.

`  transactionInfo  `

`  object ( TransactionInfo  ` )

Output only. \[Alpha\] Information of the multi-statement transaction if this job is part of one.

This property is only expected on a child job or a job that is in a session. A script parent job is not part of the transaction started in the script.

`  sessionInfo  `

`  object ( SessionInfo  ` )

Output only. Information of the session if this job is part of one.

`  finalExecutionDurationMs  `

`  string ( int64 format)  `

Output only. The duration in milliseconds of the execution of the final attempt of this job, as BigQuery may internally re-attempt to execute the job.

`  edition  `

`  enum ( ReservationEdition  ` )

Output only. Name of edition corresponding to the reservation for this job at the time of this update.

## JobStatistics2

Statistics for a query job.

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
  &quot;queryPlan&quot;: [
    {
      object (ExplainQueryStage)
    }
  ],
  &quot;estimatedBytesProcessed&quot;: string,
  &quot;timeline&quot;: [
    {
      object (QueryTimelineSample)
    }
  ],
  &quot;totalPartitionsProcessed&quot;: string,
  &quot;totalBytesProcessed&quot;: string,
  &quot;totalBytesProcessedAccuracy&quot;: string,
  &quot;totalBytesBilled&quot;: string,
  &quot;billingTier&quot;: integer,
  &quot;totalSlotMs&quot;: string,
  &quot;reservationUsage&quot;: [
    {
      &quot;name&quot;: string,
      &quot;slotMs&quot;: string
    }
  ],
  &quot;cacheHit&quot;: boolean,
  &quot;referencedTables&quot;: [
    {
      object (TableReference)
    }
  ],
  &quot;referencedRoutines&quot;: [
    {
      object (RoutineReference)
    }
  ],
  &quot;schema&quot;: {
    object (TableSchema)
  },
  &quot;numDmlAffectedRows&quot;: string,
  &quot;dmlStats&quot;: {
    object (DmlStats)
  },
  &quot;undeclaredQueryParameters&quot;: [
    {
      object (QueryParameter)
    }
  ],
  &quot;statementType&quot;: string,
  &quot;ddlOperationPerformed&quot;: string,
  &quot;ddlTargetTable&quot;: {
    object (TableReference)
  },
  &quot;ddlDestinationTable&quot;: {
    object (TableReference)
  },
  &quot;ddlTargetRowAccessPolicy&quot;: {
    object (RowAccessPolicyReference)
  },
  &quot;ddlAffectedRowAccessPolicyCount&quot;: string,
  &quot;ddlTargetRoutine&quot;: {
    object (RoutineReference)
  },
  &quot;ddlTargetDataset&quot;: {
    object (DatasetReference)
  },
  &quot;mlStatistics&quot;: {
    object (MlStatistics)
  },
  &quot;exportDataStatistics&quot;: {
    object (ExportDataStatistics)
  },
  &quot;externalServiceCosts&quot;: [
    {
      object (ExternalServiceCost)
    }
  ],
  &quot;biEngineStatistics&quot;: {
    object (BiEngineStatistics)
  },
  &quot;loadQueryStatistics&quot;: {
    object (LoadQueryStatistics)
  },
  &quot;dclTargetTable&quot;: {
    object (TableReference)
  },
  &quot;dclTargetView&quot;: {
    object (TableReference)
  },
  &quot;dclTargetDataset&quot;: {
    object (DatasetReference)
  },
  &quot;searchStatistics&quot;: {
    object (SearchStatistics)
  },
  &quot;vectorSearchStatistics&quot;: {
    object (VectorSearchStatistics)
  },
  &quot;performanceInsights&quot;: {
    object (PerformanceInsights)
  },
  &quot;queryInfo&quot;: {
    object (QueryInfo)
  },
  &quot;sparkStatistics&quot;: {
    object (SparkStatistics)
  },
  &quot;transferredBytes&quot;: string,
  &quot;materializedViewStatistics&quot;: {
    object (MaterializedViewStatistics)
  },
  &quot;metadataCacheStatistics&quot;: {
    object (MetadataCacheStatistics)
  },
  &quot;totalServicesSkuSlotMs&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  queryPlan[]  `

`  object ( ExplainQueryStage  ` )

Output only. Describes execution plan for the query.

`  estimatedBytesProcessed  `

`  string ( Int64Value format)  `

Output only. The original estimate of bytes processed for the job.

`  timeline[]  `

`  object ( QueryTimelineSample  ` )

Output only. Describes a timeline of job execution.

`  totalPartitionsProcessed  `

`  string ( Int64Value format)  `

Output only. Total number of partitions processed from all partitioned tables referenced in the job.

`  totalBytesProcessed  `

`  string ( Int64Value format)  `

Output only. Total bytes processed for the job.

`  totalBytesProcessedAccuracy  `

`  string  `

Output only. For dry-run jobs, totalBytesProcessed is an estimate and this field specifies the accuracy of the estimate. Possible values can be: UNKNOWN: accuracy of the estimate is unknown. PRECISE: estimate is precise. LOWER\_BOUND: estimate is lower bound of what the query would cost. UPPER\_BOUND: estimate is upper bound of what the query would cost.

`  totalBytesBilled  `

`  string ( Int64Value format)  `

Output only. If the project is configured to use on-demand pricing, then this field contains the total bytes billed for the job. If the project is configured to use flat-rate pricing, then you are not billed for bytes and this field is informational only.

`  billingTier  `

`  integer  `

Output only. Billing tier for the job. This is a BigQuery-specific concept which is not related to the Google Cloud notion of "free tier". The value here is a measure of the query's resource consumption relative to the amount of data scanned. For on-demand queries, the limit is 100, and all queries within this limit are billed at the standard on-demand rates. On-demand queries that exceed this limit will fail with a billingTierLimitExceeded error.

`  totalSlotMs  `

`  string ( Int64Value format)  `

Output only. Slot-milliseconds for the job.

`  reservationUsage[] (deprecated)  `

`  object  `

This item is deprecated\!

Output only. Job resource usage breakdown by reservation. This field reported misleading information and will no longer be populated.

`  reservationUsage[] (deprecated) .name  `

`  string  `

Reservation name or "unreserved" for on-demand resource usage and multi-statement queries.

`  reservationUsage[] (deprecated) .slotMs  `

`  string ( Int64Value format)  `

Total slot milliseconds used by the reservation for a particular job.

`  cacheHit  `

`  boolean  `

Output only. Whether the query result was fetched from the query cache.

`  referencedTables[]  `

`  object ( TableReference  ` )

Output only. Referenced tables for the job.

`  referencedRoutines[]  `

`  object ( RoutineReference  ` )

Output only. Referenced routines for the job.

`  schema  `

`  object ( TableSchema  ` )

Output only. The schema of the results. Present only for successful dry run of non-legacy SQL queries.

`  numDmlAffectedRows  `

`  string ( Int64Value format)  `

Output only. The number of rows affected by a DML statement. Present only for DML statements INSERT, UPDATE or DELETE.

`  dmlStats  `

`  object ( DmlStats  ` )

Output only. Detailed statistics for DML statements INSERT, UPDATE, DELETE, MERGE or TRUNCATE.

`  undeclaredQueryParameters[]  `

`  object ( QueryParameter  ` )

Output only. GoogleSQL only: list of undeclared query parameters detected during a dry run validation.

`  statementType  `

`  string  `

Output only. The type of query statement, if valid. Possible values:

  - `  SELECT  ` : [`  SELECT  `](https://cloud.google.com/bigquery/docs/reference/standard-sql/query-syntax#select_list) statement.
  - `  ASSERT  ` : [`  ASSERT  `](https://cloud.google.com/bigquery/docs/reference/standard-sql/debugging-statements#assert) statement.
  - `  INSERT  ` : [`  INSERT  `](https://cloud.google.com/bigquery/docs/reference/standard-sql/dml-syntax#insert_statement) statement.
  - `  UPDATE  ` : [`  UPDATE  `](https://cloud.google.com/bigquery/docs/reference/standard-sql/dml-syntax#update_statement) statement.
  - `  DELETE  ` : [`  DELETE  `](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-manipulation-language) statement.
  - `  MERGE  ` : [`  MERGE  `](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-manipulation-language) statement.
  - `  CREATE_TABLE  ` : [`  CREATE TABLE  `](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_table_statement) statement, without `  AS SELECT  ` .
  - `  CREATE_TABLE_AS_SELECT  ` : [`  CREATE TABLE AS SELECT  `](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_table_statement) statement.
  - `  CREATE_VIEW  ` : [`  CREATE VIEW  `](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_view_statement) statement.
  - `  CREATE_MODEL  ` : [`  CREATE MODEL  `](https://cloud.google.com/bigquery-ml/docs/reference/standard-sql/bigqueryml-syntax-create#create_model_statement) statement.
  - `  CREATE_MATERIALIZED_VIEW  ` : [`  CREATE MATERIALIZED VIEW  `](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_materialized_view_statement) statement.
  - `  CREATE_FUNCTION  ` : [`  CREATE FUNCTION  `](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_function_statement) statement.
  - `  CREATE_TABLE_FUNCTION  ` : [`  CREATE TABLE FUNCTION  `](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_table_function_statement) statement.
  - `  CREATE_PROCEDURE  ` : [`  CREATE PROCEDURE  `](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_procedure) statement.
  - `  CREATE_ROW_ACCESS_POLICY  ` : [`  CREATE ROW ACCESS POLICY  `](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_row_access_policy_statement) statement.
  - `  CREATE_SCHEMA  ` : [`  CREATE SCHEMA  `](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_schema_statement) statement.
  - `  CREATE_SNAPSHOT_TABLE  ` : [`  CREATE SNAPSHOT TABLE  `](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_snapshot_table_statement) statement.
  - `  CREATE_SEARCH_INDEX  ` : [`  CREATE SEARCH INDEX  `](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_search_index_statement) statement.
  - `  DROP_TABLE  ` : [`  DROP TABLE  `](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#drop_table_statement) statement.
  - `  DROP_EXTERNAL_TABLE  ` : [`  DROP EXTERNAL TABLE  `](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#drop_external_table_statement) statement.
  - `  DROP_VIEW  ` : [`  DROP VIEW  `](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#drop_view_statement) statement.
  - `  DROP_MODEL  ` : [`  DROP MODEL  `](https://cloud.google.com/bigquery-ml/docs/reference/standard-sql/bigqueryml-syntax-drop-model) statement.
  - `  DROP_MATERIALIZED_VIEW  ` : [`  DROP MATERIALIZED VIEW  `](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#drop_materialized_view_statement) statement.
  - `  DROP_FUNCTION  ` : [`  DROP FUNCTION  `](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#drop_function_statement) statement.
  - `  DROP_TABLE_FUNCTION  ` : [`  DROP TABLE FUNCTION  `](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#drop_table_function) statement.
  - `  DROP_PROCEDURE  ` : [`  DROP PROCEDURE  `](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#drop_procedure_statement) statement.
  - `  DROP_SEARCH_INDEX  ` : [`  DROP SEARCH INDEX  `](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#drop_search_index) statement.
  - `  DROP_SCHEMA  ` : [`  DROP SCHEMA  `](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#drop_schema_statement) statement.
  - `  DROP_SNAPSHOT_TABLE  ` : [`  DROP SNAPSHOT TABLE  `](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#drop_snapshot_table_statement) statement.
  - `  DROP_ROW_ACCESS_POLICY  ` : [`  DROP [ALL] ROW ACCESS POLICY|POLICIES  `](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#drop_row_access_policy_statement) statement.
  - `  ALTER_TABLE  ` : [`  ALTER TABLE  `](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#alter_table_set_options_statement) statement.
  - `  ALTER_VIEW  ` : [`  ALTER VIEW  `](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#alter_view_set_options_statement) statement.
  - `  ALTER_MATERIALIZED_VIEW  ` : [`  ALTER MATERIALIZED VIEW  `](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#alter_materialized_view_set_options_statement) statement.
  - `  ALTER_SCHEMA  ` : [`  ALTER SCHEMA  `](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#alter_schema_set_options_statement) statement.
  - `  SCRIPT  ` : [`  SCRIPT  `](https://cloud.google.com/bigquery/docs/reference/standard-sql/procedural-language) .
  - `  TRUNCATE_TABLE  ` : [`  TRUNCATE TABLE  `](https://cloud.google.com/bigquery/docs/reference/standard-sql/dml-syntax#truncate_table_statement) statement.
  - `  CREATE_EXTERNAL_TABLE  ` : [`  CREATE EXTERNAL TABLE  `](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_external_table_statement) statement.
  - `  EXPORT_DATA  ` : [`  EXPORT DATA  `](https://cloud.google.com/bigquery/docs/reference/standard-sql/other-statements#export_data_statement) statement.
  - `  EXPORT_MODEL  ` : [`  EXPORT MODEL  `](https://cloud.google.com/bigquery-ml/docs/reference/standard-sql/bigqueryml-syntax-export-model) statement.
  - `  LOAD_DATA  ` : [`  LOAD DATA  `](https://cloud.google.com/bigquery/docs/reference/standard-sql/other-statements#load_data_statement) statement.
  - `  CALL  ` : [`  CALL  `](https://cloud.google.com/bigquery/docs/reference/standard-sql/procedural-language#call) statement.

`  ddlOperationPerformed  `

`  string  `

Output only. The DDL operation performed, possibly dependent on the pre-existence of the DDL target.

`  ddlTargetTable  `

`  object ( TableReference  ` )

Output only. The DDL target table. Present only for CREATE/DROP TABLE/VIEW and DROP ALL ROW ACCESS POLICIES queries.

`  ddlDestinationTable  `

`  object ( TableReference  ` )

Output only. The table after rename. Present only for ALTER TABLE RENAME TO query.

`  ddlTargetRowAccessPolicy  `

`  object ( RowAccessPolicyReference  ` )

Output only. The DDL target row access policy. Present only for CREATE/DROP ROW ACCESS POLICY queries.

`  ddlAffectedRowAccessPolicyCount  `

`  string ( Int64Value format)  `

Output only. The number of row access policies affected by a DDL statement. Present only for DROP ALL ROW ACCESS POLICIES queries.

`  ddlTargetRoutine  `

`  object ( RoutineReference  ` )

Output only. \[Beta\] The DDL target routine. Present only for CREATE/DROP FUNCTION/PROCEDURE queries.

`  ddlTargetDataset  `

`  object ( DatasetReference  ` )

Output only. The DDL target dataset. Present only for CREATE/ALTER/DROP SCHEMA(dataset) queries.

`  mlStatistics  `

`  object ( MlStatistics  ` )

Output only. Statistics of a BigQuery ML training job.

`  exportDataStatistics  `

`  object ( ExportDataStatistics  ` )

Output only. Stats for EXPORT DATA statement.

`  externalServiceCosts[]  `

`  object ( ExternalServiceCost  ` )

Output only. Job cost breakdown as bigquery internal cost and external service costs.

`  biEngineStatistics  `

`  object ( BiEngineStatistics  ` )

Output only. BI Engine specific Statistics.

`  loadQueryStatistics  `

`  object ( LoadQueryStatistics  ` )

Output only. Statistics for a LOAD query.

`  dclTargetTable  `

`  object ( TableReference  ` )

Output only. Referenced table for DCL statement.

`  dclTargetView  `

`  object ( TableReference  ` )

Output only. Referenced view for DCL statement.

`  dclTargetDataset  `

`  object ( DatasetReference  ` )

Output only. Referenced dataset for DCL statement.

`  searchStatistics  `

`  object ( SearchStatistics  ` )

Output only. Search query specific statistics.

`  vectorSearchStatistics  `

`  object ( VectorSearchStatistics  ` )

Output only. Vector Search query specific statistics.

`  performanceInsights  `

`  object ( PerformanceInsights  ` )

Output only. Performance insights.

`  queryInfo  `

`  object ( QueryInfo  ` )

Output only. jobs.query optimization information for a QUERY job.

`  sparkStatistics  `

`  object ( SparkStatistics  ` )

Output only. Statistics of a Spark procedure job.

`  transferredBytes  `

`  string ( Int64Value format)  `

Output only. Total bytes transferred for cross-cloud queries such as Cross Cloud Transfer and CREATE TABLE AS SELECT (CTAS).

`  materializedViewStatistics  `

`  object ( MaterializedViewStatistics  ` )

Output only. Statistics of materialized views of a query job.

`  metadataCacheStatistics  `

`  object ( MetadataCacheStatistics  ` )

Output only. Statistics of metadata cache usage in a query for BigLake tables.

`  totalServicesSkuSlotMs  `

`  string ( int64 format)  `

Output only. Total slot milliseconds for the job that ran on external services and billed on the services SKU. This field is only populated for jobs that have external service costs, and is the total of the usage for costs whose billing method is `  "SERVICES_SKU"  ` .

## ExplainQueryStage

A single stage of query execution.

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
  &quot;id&quot;: string,
  &quot;startMs&quot;: string,
  &quot;endMs&quot;: string,
  &quot;inputStages&quot;: [
    string
  ],
  &quot;waitRatioAvg&quot;: number,
  &quot;waitMsAvg&quot;: string,
  &quot;waitRatioMax&quot;: number,
  &quot;waitMsMax&quot;: string,
  &quot;readRatioAvg&quot;: number,
  &quot;readMsAvg&quot;: string,
  &quot;readRatioMax&quot;: number,
  &quot;readMsMax&quot;: string,
  &quot;computeRatioAvg&quot;: number,
  &quot;computeMsAvg&quot;: string,
  &quot;computeRatioMax&quot;: number,
  &quot;computeMsMax&quot;: string,
  &quot;writeRatioAvg&quot;: number,
  &quot;writeMsAvg&quot;: string,
  &quot;writeRatioMax&quot;: number,
  &quot;writeMsMax&quot;: string,
  &quot;shuffleOutputBytes&quot;: string,
  &quot;shuffleOutputBytesSpilled&quot;: string,
  &quot;recordsRead&quot;: string,
  &quot;recordsWritten&quot;: string,
  &quot;parallelInputs&quot;: string,
  &quot;completedParallelInputs&quot;: string,
  &quot;status&quot;: string,
  &quot;steps&quot;: [
    {
      object (ExplainQueryStep)
    }
  ],
  &quot;slotMs&quot;: string,
  &quot;computeMode&quot;: enum (ComputeMode)
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  name  `

`  string  `

Human-readable name for the stage.

`  id  `

`  string ( Int64Value format)  `

Unique ID for the stage within the plan.

`  startMs  `

`  string ( int64 format)  `

Stage start time represented as milliseconds since the epoch.

`  endMs  `

`  string ( int64 format)  `

Stage end time represented as milliseconds since the epoch.

`  inputStages[]  `

`  string ( int64 format)  `

IDs for stages that are inputs to this stage.

`  waitRatioAvg  `

`  number  `

Relative amount of time the average shard spent waiting to be scheduled.

`  waitMsAvg  `

`  string ( Int64Value format)  `

Milliseconds the average shard spent waiting to be scheduled.

`  waitRatioMax  `

`  number  `

Relative amount of time the slowest shard spent waiting to be scheduled.

`  waitMsMax  `

`  string ( Int64Value format)  `

Milliseconds the slowest shard spent waiting to be scheduled.

`  readRatioAvg  `

`  number  `

Relative amount of time the average shard spent reading input.

`  readMsAvg  `

`  string ( Int64Value format)  `

Milliseconds the average shard spent reading input.

`  readRatioMax  `

`  number  `

Relative amount of time the slowest shard spent reading input.

`  readMsMax  `

`  string ( Int64Value format)  `

Milliseconds the slowest shard spent reading input.

`  computeRatioAvg  `

`  number  `

Relative amount of time the average shard spent on CPU-bound tasks.

`  computeMsAvg  `

`  string ( Int64Value format)  `

Milliseconds the average shard spent on CPU-bound tasks.

`  computeRatioMax  `

`  number  `

Relative amount of time the slowest shard spent on CPU-bound tasks.

`  computeMsMax  `

`  string ( Int64Value format)  `

Milliseconds the slowest shard spent on CPU-bound tasks.

`  writeRatioAvg  `

`  number  `

Relative amount of time the average shard spent on writing output.

`  writeMsAvg  `

`  string ( Int64Value format)  `

Milliseconds the average shard spent on writing output.

`  writeRatioMax  `

`  number  `

Relative amount of time the slowest shard spent on writing output.

`  writeMsMax  `

`  string ( Int64Value format)  `

Milliseconds the slowest shard spent on writing output.

`  shuffleOutputBytes  `

`  string ( Int64Value format)  `

Total number of bytes written to shuffle.

`  shuffleOutputBytesSpilled  `

`  string ( Int64Value format)  `

Total number of bytes written to shuffle and spilled to disk.

`  recordsRead  `

`  string ( Int64Value format)  `

Number of records read into the stage.

`  recordsWritten  `

`  string ( Int64Value format)  `

Number of records written by the stage.

`  parallelInputs  `

`  string ( Int64Value format)  `

Number of parallel input segments to be processed

`  completedParallelInputs  `

`  string ( Int64Value format)  `

Number of parallel input segments completed.

`  status  `

`  string  `

Current status for this stage.

`  steps[]  `

`  object ( ExplainQueryStep  ` )

tabledata.list of operations within the stage in dependency order (approximately chronological).

`  slotMs  `

`  string ( Int64Value format)  `

Slot-milliseconds used by the stage.

`  computeMode  `

`  enum ( ComputeMode  ` )

Output only. Compute mode for this stage.

## ExplainQueryStep

An operation within a stage.

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
  &quot;kind&quot;: string,
  &quot;substeps&quot;: [
    string
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  kind  `

`  string  `

Machine-readable operation type.

`  substeps[]  `

`  string  `

Human-readable description of the step(s).

## ComputeMode

Indicates the type of compute mode.

Enums

`  COMPUTE_MODE_UNSPECIFIED  `

ComputeMode type not specified.

`  BIGQUERY  `

This stage was processed using BigQuery slots.

`  BI_ENGINE  `

This stage was processed using BI Engine compute.

## QueryTimelineSample

Summary of the state of query execution at a given time.

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
  &quot;elapsedMs&quot;: string,
  &quot;totalSlotMs&quot;: string,
  &quot;pendingUnits&quot;: string,
  &quot;completedUnits&quot;: string,
  &quot;activeUnits&quot;: string,
  &quot;estimatedRunnableUnits&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  elapsedMs  `

`  string ( Int64Value format)  `

Milliseconds elapsed since the start of query execution.

`  totalSlotMs  `

`  string ( Int64Value format)  `

Cumulative slot-ms consumed by the query.

`  pendingUnits  `

`  string ( Int64Value format)  `

Total units of work remaining for the query. This number can be revised (increased or decreased) while the query is running.

`  completedUnits  `

`  string ( Int64Value format)  `

Total parallel units of work completed by this query.

`  activeUnits  `

`  string ( Int64Value format)  `

Total number of active workers. This does not correspond directly to slot usage. This is the largest value observed since the last sample.

`  estimatedRunnableUnits  `

`  string ( Int64Value format)  `

Units of work that can be scheduled immediately. Providing additional slots for these units of work will accelerate the query, if no other query in the reservation needs additional slots.

## MlStatistics

Job statistics specific to a BigQuery ML training job.

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
  &quot;maxIterations&quot;: string,
  &quot;iterationResults&quot;: [
    {
      object (IterationResult)
    }
  ],
  &quot;modelType&quot;: enum (ModelType),
  &quot;trainingType&quot;: enum (TrainingType),
  &quot;hparamTrials&quot;: [
    {
      object (HparamTuningTrial)
    }
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  maxIterations  `

`  string ( int64 format)  `

Output only. Maximum number of iterations specified as maxIterations in the 'CREATE MODEL' query. The actual number of iterations may be less than this number due to early stop.

`  iterationResults[]  `

`  object ( IterationResult  ` )

Results for all completed iterations. Empty for [hyperparameter tuning jobs](https://cloud.google.com/bigquery-ml/docs/reference/standard-sql/bigqueryml-syntax-hp-tuning-overview) .

`  modelType  `

`  enum ( ModelType  ` )

Output only. The type of the model that is being trained.

`  trainingType  `

`  enum ( TrainingType  ` )

Output only. Training type of the job.

`  hparamTrials[]  `

`  object ( HparamTuningTrial  ` )

Output only. Trials of a [hyperparameter tuning job](https://cloud.google.com/bigquery-ml/docs/reference/standard-sql/bigqueryml-syntax-hp-tuning-overview) sorted by trialId.

## TrainingType

Training type.

Enums

`  TRAINING_TYPE_UNSPECIFIED  `

Unspecified training type.

`  SINGLE_TRAINING  `

Single training with fixed parameter space.

`  HPARAM_TUNING  `

[Hyperparameter tuning training](https://cloud.google.com/bigquery-ml/docs/reference/standard-sql/bigqueryml-syntax-hp-tuning-overview) .

## ExportDataStatistics

Statistics for the EXPORT DATA statement as part of jobs.query Job. EXTRACT JOB statistics are populated in JobStatistics4.

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
  &quot;fileCount&quot;: string,
  &quot;rowCount&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  fileCount  `

`  string ( Int64Value format)  `

Number of destination files generated in case of EXPORT DATA statement only.

`  rowCount  `

`  string ( Int64Value format)  `

\[Alpha\] Number of destination rows generated in case of EXPORT DATA statement only.

## ExternalServiceCost

The external service cost is a portion of the total cost, these costs are not additive with totalBytesBilled. Moreover, this field only track external service costs that will show up as BigQuery costs (e.g. training BigQuery ML job with google cloud CAIP or Automl Tables services), not other costs which may be accrued by running the query (e.g. reading from Bigtable or Cloud Storage). The external service costs with different billing sku (e.g. CAIP job is charged based on VM usage) are converted to BigQuery billed\_bytes and slotMs with equivalent amount of US dollars. Services may not directly correlate to these metrics, but these are the equivalents for billing purposes. Output only.

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
  &quot;externalService&quot;: string,
  &quot;bytesProcessed&quot;: string,
  &quot;bytesBilled&quot;: string,
  &quot;slotMs&quot;: string,
  &quot;reservedSlotCount&quot;: string,
  &quot;billingMethod&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  externalService  `

`  string  `

External service name.

`  bytesProcessed  `

`  string ( Int64Value format)  `

External service cost in terms of bigquery bytes processed.

`  bytesBilled  `

`  string ( Int64Value format)  `

External service cost in terms of bigquery bytes billed.

`  slotMs  `

`  string ( Int64Value format)  `

External service cost in terms of bigquery slot milliseconds.

`  reservedSlotCount  `

`  string ( int64 format)  `

Non-preemptable reserved slots used for external job. For example, reserved slots for Cloua AI Platform job are the VM usages converted to BigQuery slot with equivalent mount of price.

`  billingMethod  `

`  string  `

The billing method used for the external job. This field, set to `  SERVICES_SKU  ` , is only used when billing under the services SKU. Otherwise, it is unspecified for backward compatibility.

## BiEngineStatistics

Statistics for a BI Engine specific query. Populated as part of JobStatistics2

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
  &quot;biEngineMode&quot;: enum (BiEngineMode),
  &quot;accelerationMode&quot;: enum (BiEngineAccelerationMode),
  &quot;biEngineReasons&quot;: [
    {
      object (BiEngineReason)
    }
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  biEngineMode  `

`  enum ( BiEngineMode  ` )

Output only. Specifies which mode of BI Engine acceleration was performed (if any).

`  accelerationMode  `

`  enum ( BiEngineAccelerationMode  ` )

Output only. Specifies which mode of BI Engine acceleration was performed (if any).

`  biEngineReasons[]  `

`  object ( BiEngineReason  ` )

In case of DISABLED or PARTIAL biEngineMode, these contain the explanatory reasons as to why BI Engine could not accelerate. In case the full query was accelerated, this field is not populated.

## BiEngineMode

Indicates the type of BI Engine acceleration.

Enums

`  ACCELERATION_MODE_UNSPECIFIED  `

BiEngineMode type not specified.

`  DISABLED  `

BI Engine disabled the acceleration. biEngineReasons specifies a more detailed reason.

`  PARTIAL  `

Part of the query was accelerated using BI Engine. See biEngineReasons for why parts of the query were not accelerated.

`  FULL  `

All of the query was accelerated using BI Engine.

## BiEngineAccelerationMode

Indicates the type of BI Engine acceleration.

Enums

`  BI_ENGINE_ACCELERATION_MODE_UNSPECIFIED  `

BiEngineMode type not specified.

`  BI_ENGINE_DISABLED  `

BI Engine acceleration was attempted but disabled. biEngineReasons specifies a more detailed reason.

`  PARTIAL_INPUT  `

Some inputs were accelerated using BI Engine. See biEngineReasons for why parts of the query were not accelerated.

`  FULL_INPUT  `

All of the query inputs were accelerated using BI Engine.

`  FULL_QUERY  `

All of the query was accelerated using BI Engine.

## BiEngineReason

Reason why BI Engine didn't accelerate the query (or sub-query).

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
  &quot;code&quot;: enum (Code),
  &quot;message&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  code  `

`  enum ( Code  ` )

Output only. High-level BI Engine reason for partial or disabled acceleration

`  message  `

`  string  `

Output only. Free form human-readable reason for partial or disabled acceleration.

## Code

Indicates the high-level reason for no/partial acceleration

Enums

`  CODE_UNSPECIFIED  `

BiEngineReason not specified.

`  NO_RESERVATION  `

No reservation available for BI Engine acceleration.

`  INSUFFICIENT_RESERVATION  `

Not enough memory available for BI Engine acceleration.

`  UNSUPPORTED_SQL_TEXT  `

This particular SQL text is not supported for acceleration by BI Engine.

`  INPUT_TOO_LARGE  `

Input too large for acceleration by BI Engine.

`  OTHER_REASON  `

Catch-all code for all other cases for partial or disabled acceleration.

`  TABLE_EXCLUDED  `

One or more tables were not eligible for BI Engine acceleration.

## LoadQueryStatistics

Statistics for a LOAD query.

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
  &quot;inputFiles&quot;: string,
  &quot;inputFileBytes&quot;: string,
  &quot;outputRows&quot;: string,
  &quot;outputBytes&quot;: string,
  &quot;badRecords&quot;: string,
  &quot;bytesTransferred&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  inputFiles  `

`  string ( Int64Value format)  `

Output only. Number of source files in a LOAD query.

`  inputFileBytes  `

`  string ( Int64Value format)  `

Output only. Number of bytes of source data in a LOAD query.

`  outputRows  `

`  string ( Int64Value format)  `

Output only. Number of rows imported in a LOAD query. Note that while a LOAD query is in the running state, this value may change.

`  outputBytes  `

`  string ( Int64Value format)  `

Output only. Size of the loaded data in bytes. Note that while a LOAD query is in the running state, this value may change.

`  badRecords  `

`  string ( Int64Value format)  `

Output only. The number of bad records encountered while processing a LOAD query. Note that if the job has failed because of more bad records encountered than the maximum allowed in the load job configuration, then this number can be less than the total number of bad records present in the input data.

`  bytesTransferred (deprecated)  `

`  string ( Int64Value format)  `

This item is deprecated\!

Output only. This field is deprecated. The number of bytes of source data copied over the network for a `  LOAD  ` query. `  transferredBytes  ` has the canonical value for physical transferred bytes, which is used for BigQuery Omni billing.

## SearchStatistics

Statistics for a search query. Populated as part of JobStatistics2.

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
  &quot;indexUsageMode&quot;: enum (IndexUsageMode),
  &quot;indexUnusedReasons&quot;: [
    {
      object (IndexUnusedReason)
    }
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  indexUsageMode  `

`  enum ( IndexUsageMode  ` )

Specifies the index usage mode for the query.

`  indexUnusedReasons[]  `

`  object ( IndexUnusedReason  ` )

When `  indexUsageMode  ` is `  UNUSED  ` or `  PARTIALLY_USED  ` , this field explains why indexes were not used in all or part of the search query. If `  indexUsageMode  ` is `  FULLY_USED  ` , this field is not populated.

## IndexUsageMode

Indicates the type of search index usage in the entire search query.

Enums

`  INDEX_USAGE_MODE_UNSPECIFIED  `

Index usage mode not specified.

`  UNUSED  `

No search indexes were used in the search query. See [`  indexUnusedReasons  `](/bigquery/docs/reference/rest/v2/Job#IndexUnusedReason) for detailed reasons.

`  PARTIALLY_USED  `

Part of the search query used search indexes. See [`  indexUnusedReasons  `](/bigquery/docs/reference/rest/v2/Job#IndexUnusedReason) for why other parts of the query did not use search indexes.

`  FULLY_USED  `

The entire search query used search indexes.

## IndexUnusedReason

Reason about why no search index was used in the search query (or sub-query).

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
  &quot;code&quot;: enum (Code),
  &quot;message&quot;: string,
  &quot;baseTable&quot;: {
    object (TableReference)
  },
  &quot;indexName&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  code  `

`  enum ( Code  ` )

Specifies the high-level reason for the scenario when no search index was used.

`  message  `

`  string  `

Free form human-readable reason for the scenario when no search index was used.

`  baseTable  `

`  object ( TableReference  ` )

Specifies the base table involved in the reason that no search index was used.

`  indexName  `

`  string  `

Specifies the name of the unused search index, if available.

## Code

Indicates the high-level reason for the scenario when no search index was used.

Enums

`  CODE_UNSPECIFIED  `

Code not specified.

`  INDEX_CONFIG_NOT_AVAILABLE  `

Indicates the search index configuration has not been created.

`  PENDING_INDEX_CREATION  `

Indicates the search index creation has not been completed.

`  BASE_TABLE_TRUNCATED  `

Indicates the base table has been truncated (rows have been removed from table with TRUNCATE TABLE statement) since the last time the search index was refreshed.

`  INDEX_CONFIG_MODIFIED  `

Indicates the search index configuration has been changed since the last time the search index was refreshed.

`  TIME_TRAVEL_QUERY  `

Indicates the search query accesses data at a timestamp before the last time the search index was refreshed.

`  NO_PRUNING_POWER  `

Indicates the usage of search index will not contribute to any pruning improvement for the search function, e.g. when the search predicate is in a disjunction with other non-search predicates.

`  UNINDEXED_SEARCH_FIELDS  `

Indicates the search index does not cover all fields in the search function.

`  UNSUPPORTED_SEARCH_PATTERN  `

Indicates the search index does not support the given search query pattern.

`  OPTIMIZED_WITH_MATERIALIZED_VIEW  `

Indicates the query has been optimized by using a materialized view.

`  SECURED_BY_DATA_MASKING  `

Indicates the query has been secured by data masking, and thus search indexes are not applicable.

`  MISMATCHED_TEXT_ANALYZER  `

Indicates that the search index and the search function call do not have the same text analyzer.

`  BASE_TABLE_TOO_SMALL  `

Indicates the base table is too small (below a certain threshold). The index does not provide noticeable search performance gains when the base table is too small.

`  BASE_TABLE_TOO_LARGE  `

Indicates that the total size of indexed base tables in your organization exceeds your region's limit and the index is not used in the query. To index larger base tables, you can [use your own reservation](https://cloud.google.com/bigquery/docs/search-index#use_your_own_reservation) for index-management jobs.

`  ESTIMATED_PERFORMANCE_GAIN_TOO_LOW  `

Indicates that the estimated performance gain from using the search index is too low for the given search query.

`  COLUMN_METADATA_INDEX_NOT_USED  `

Indicates that the column metadata index (which the search index depends on) is not used. User can refer to the [column metadata index usage](https://cloud.google.com/bigquery/docs/metadata-indexing-managed-tables#view_column_metadata_index_usage) for more details on why it was not used.

`  INDEX_SUPPRESSED_BY_FUNCTION_OPTION  `

Indicates that an option in the search function that cannot make use of the index has been selected.

`  QUERY_CACHE_HIT  `

Indicates that the query was cached, and thus the search index was not used.

`  STALE_INDEX  `

The index cannot be used in the search query because it is stale.

`  INTERNAL_ERROR  `

Indicates an internal error that causes the search index to be unused.

`  OTHER_REASON  `

Indicates that the reason search indexes cannot be used in the query is not covered by any of the other IndexUnusedReason options.

## VectorSearchStatistics

Statistics for a vector search query. Populated as part of JobStatistics2.

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
  &quot;indexUsageMode&quot;: enum (IndexUsageMode),
  &quot;indexUnusedReasons&quot;: [
    {
      object (IndexUnusedReason)
    }
  ],
  &quot;storedColumnsUsages&quot;: [
    {
      object (StoredColumnsUsage)
    }
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  indexUsageMode  `

`  enum ( IndexUsageMode  ` )

Specifies the index usage mode for the query.

`  indexUnusedReasons[]  `

`  object ( IndexUnusedReason  ` )

When `  indexUsageMode  ` is `  UNUSED  ` or `  PARTIALLY_USED  ` , this field explains why indexes were not used in all or part of the vector search query. If `  indexUsageMode  ` is `  FULLY_USED  ` , this field is not populated.

`  storedColumnsUsages[]  `

`  object ( StoredColumnsUsage  ` )

Specifies the usage of stored columns in the query when stored columns are used in the query.

## IndexUsageMode

Indicates the type of vector index usage in the entire vector search query.

Enums

`  INDEX_USAGE_MODE_UNSPECIFIED  `

Index usage mode not specified.

`  UNUSED  `

No vector indexes were used in the vector search query. See [`  indexUnusedReasons  `](/bigquery/docs/reference/rest/v2/Job#IndexUnusedReason) for detailed reasons.

`  PARTIALLY_USED  `

Part of the vector search query used vector indexes. See [`  indexUnusedReasons  `](/bigquery/docs/reference/rest/v2/Job#IndexUnusedReason) for why other parts of the query did not use vector indexes.

`  FULLY_USED  `

The entire vector search query used vector indexes.

## StoredColumnsUsage

Indicates the stored columns usage in the query.

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
  &quot;storedColumnsUnusedReasons&quot;: [
    {
      object (StoredColumnsUnusedReason)
    }
  ],
  &quot;isQueryAccelerated&quot;: boolean,
  &quot;baseTable&quot;: {
    object (TableReference)
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  storedColumnsUnusedReasons[]  `

`  object ( StoredColumnsUnusedReason  ` )

If stored columns were not used, explain why.

`  isQueryAccelerated  `

`  boolean  `

Specifies whether the query was accelerated with stored columns.

`  baseTable  `

`  object ( TableReference  ` )

Specifies the base table.

## StoredColumnsUnusedReason

If the stored column was not used, explain why.

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
  &quot;uncoveredColumns&quot;: [
    string
  ],
  &quot;code&quot;: enum (Code),
  &quot;message&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  uncoveredColumns[]  `

`  string  `

Specifies which columns were not covered by the stored columns for the specified code up to 20 columns. This is populated when the code is STORED\_COLUMNS\_COVER\_INSUFFICIENT and BASE\_TABLE\_HAS\_CLS.

`  code  `

`  enum ( Code  ` )

Specifies the high-level reason for the unused scenario, each reason must have a code associated.

`  message  `

`  string  `

Specifies the detailed description for the scenario.

## Code

Indicates the high-level reason for the scenario when stored columns cannot be used in the query.

Enums

`  CODE_UNSPECIFIED  `

Default value.

`  STORED_COLUMNS_COVER_INSUFFICIENT  `

If stored columns do not fully cover the columns.

`  BASE_TABLE_HAS_RLS  `

If the base table has RLS (Row Level Security).

`  BASE_TABLE_HAS_CLS  `

If the base table has CLS (Column Level Security).

`  UNSUPPORTED_PREFILTER  `

If the provided prefilter is not supported.

`  INTERNAL_ERROR  `

If an internal error is preventing stored columns from being used.

`  OTHER_REASON  `

Indicates that the reason stored columns cannot be used in the query is not covered by any of the other StoredColumnsUnusedReason options.

## PerformanceInsights

Performance insights for the job.

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
  &quot;avgPreviousExecutionMs&quot;: string,
  &quot;stagePerformanceStandaloneInsights&quot;: [
    {
      object (StagePerformanceStandaloneInsight)
    }
  ],
  &quot;stagePerformanceChangeInsights&quot;: [
    {
      object (StagePerformanceChangeInsight)
    }
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  avgPreviousExecutionMs  `

`  string ( int64 format)  `

Output only. Average execution ms of previous runs. Indicates the job ran slow compared to previous executions. To find previous executions, use INFORMATION\_SCHEMA tables and filter jobs with same query hash.

`  stagePerformanceStandaloneInsights[]  `

`  object ( StagePerformanceStandaloneInsight  ` )

Output only. Standalone query stage performance insights, for exploring potential improvements.

`  stagePerformanceChangeInsights[]  `

`  object ( StagePerformanceChangeInsight  ` )

Output only. jobs.query stage performance insights compared to previous runs, for diagnosing performance regression.

## StagePerformanceStandaloneInsight

Standalone performance insights for a specific stage.

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
  &quot;stageId&quot;: string,
  &quot;biEngineReasons&quot;: [
    {
      object (BiEngineReason)
    }
  ],
  &quot;highCardinalityJoins&quot;: [
    {
      object (HighCardinalityJoin)
    }
  ],
  &quot;slotContention&quot;: boolean,
  &quot;insufficientShuffleQuota&quot;: boolean,
  &quot;partitionSkew&quot;: {
    object (PartitionSkew)
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  stageId  `

`  string ( int64 format)  `

Output only. The stage id that the insight mapped to.

`  biEngineReasons[]  `

`  object ( BiEngineReason  ` )

Output only. If present, the stage had the following reasons for being disqualified from BI Engine execution.

`  highCardinalityJoins[]  `

`  object ( HighCardinalityJoin  ` )

Output only. High cardinality joins in the stage.

`  slotContention  `

`  boolean  `

Output only. True if the stage has a slot contention issue.

`  insufficientShuffleQuota  `

`  boolean  `

Output only. True if the stage has insufficient shuffle quota.

`  partitionSkew  `

`  object ( PartitionSkew  ` )

Output only. Partition skew in the stage.

## HighCardinalityJoin

High cardinality join detailed information.

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
  &quot;leftRows&quot;: string,
  &quot;rightRows&quot;: string,
  &quot;outputRows&quot;: string,
  &quot;stepIndex&quot;: integer
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  leftRows  `

`  string ( int64 format)  `

Output only. Count of left input rows.

`  rightRows  `

`  string ( int64 format)  `

Output only. Count of right input rows.

`  outputRows  `

`  string ( int64 format)  `

Output only. Count of the output rows.

`  stepIndex  `

`  integer  `

Output only. The index of the join operator in the ExplainQueryStep lists.

## PartitionSkew

Partition skew detailed information.

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
  &quot;skewSources&quot;: [
    {
      object (SkewSource)
    }
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  skewSources[]  `

`  object ( SkewSource  ` )

Output only. Source stages which produce skewed data.

## SkewSource

Details about source stages which produce skewed data.

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
  &quot;stageId&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  stageId  `

`  string ( int64 format)  `

Output only. Stage id of the skew source stage.

## StagePerformanceChangeInsight

Performance insights compared to the previous executions for a specific stage.

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
  &quot;stageId&quot;: string,
  &quot;inputDataChange&quot;: {
    object (InputDataChange)
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  stageId  `

`  string ( int64 format)  `

Output only. The stage id that the insight mapped to.

`  inputDataChange  `

`  object ( InputDataChange  ` )

Output only. Input data change insight of the query stage.

## InputDataChange

Details about the input data change insight.

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
  &quot;recordsReadDiffPercentage&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  recordsReadDiffPercentage  `

`  number  `

Output only. Records read difference percentage compared to a previous run.

## QueryInfo

jobs.query optimization information for a QUERY job.

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
  &quot;optimizationDetails&quot;: {
    object
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  optimizationDetails  `

`  object ( Struct  ` format)

Output only. Information about query optimizations.

## SparkStatistics

Statistics for a BigSpark query. Populated as part of JobStatistics2

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
  &quot;endpoints&quot;: {
    string: string,
    ...
  },
  &quot;sparkJobId&quot;: string,
  &quot;sparkJobLocation&quot;: string,
  &quot;loggingInfo&quot;: {
    object (LoggingInfo)
  },
  &quot;kmsKeyName&quot;: string,
  &quot;gcsStagingBucket&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  endpoints  `

`  map (key: string, value: string)  `

Output only. Endpoints returned from Dataproc. Key list: - history\_server\_endpoint: A link to Spark job UI.

`  sparkJobId  `

`  string  `

Output only. Spark job ID if a Spark job is created successfully.

`  sparkJobLocation  `

`  string  `

Output only. Location where the Spark job is executed. A location is selected by BigQueury for jobs configured to run in a multi-region.

`  loggingInfo  `

`  object ( LoggingInfo  ` )

Output only. Logging info is used to generate a link to Cloud Logging.

`  kmsKeyName  `

`  string  `

Output only. The Cloud KMS encryption key that is used to protect the resources created by the Spark job. If the Spark procedure uses the invoker security mode, the Cloud KMS encryption key is either inferred from the provided system variable, `  @@spark_proc_properties.kms_key_name  ` , or the default key of the BigQuery job's project (if the CMEK organization policy is enforced). Otherwise, the Cloud KMS key is either inferred from the Spark connection associated with the procedure (if it is provided), or from the default key of the Spark connection's project if the CMEK organization policy is enforced.

Example:

  - `  projects/[kms_project_id]/locations/[region]/keyRings/[key_region]/cryptoKeys/[key]  `

`  gcsStagingBucket  `

`  string  `

Output only. The Google Cloud Storage bucket that is used as the default file system by the Spark application. This field is only filled when the Spark procedure uses the invoker security mode. The `  gcsStagingBucket  ` bucket is inferred from the `  @@spark_proc_properties.staging_bucket  ` system variable (if it is provided). Otherwise, BigQuery creates a default staging bucket for the job and returns the bucket name in this field.

Example:

  - `  gs://[bucketName]  `

## LoggingInfo

Spark job logs can be filtered by these fields in Cloud Logging.

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
  &quot;resourceType&quot;: string,
  &quot;projectId&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  resourceType  `

`  string  `

Output only. Resource type used for logging.

`  projectId  `

`  string  `

Output only. Project ID where the Spark logs were written.

## MaterializedViewStatistics

Statistics of materialized views considered in a query job.

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
  &quot;materializedView&quot;: [
    {
      object (MaterializedView)
    }
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  materializedView[]  `

`  object ( MaterializedView  ` )

Materialized views considered for the query job. Only certain materialized views are used. For a detailed list, see the child message.

If many materialized views are considered, then the list might be incomplete.

## MaterializedView

A materialized view considered for a query job.

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
  &quot;tableReference&quot;: {
    object (TableReference)
  },
  &quot;chosen&quot;: boolean,
  &quot;estimatedBytesSaved&quot;: string,
  &quot;rejectedReason&quot;: enum (RejectedReason)
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  tableReference  `

`  object ( TableReference  ` )

The candidate materialized view.

`  chosen  `

`  boolean  `

Whether the materialized view is chosen for the query.

A materialized view can be chosen to rewrite multiple parts of the same query. If a materialized view is chosen to rewrite any part of the query, then this field is true, even if the materialized view was not chosen to rewrite others parts.

`  estimatedBytesSaved  `

`  string ( int64 format)  `

If present, specifies a best-effort estimation of the bytes saved by using the materialized view rather than its base tables.

`  rejectedReason  `

`  enum ( RejectedReason  ` )

If present, specifies the reason why the materialized view was not chosen for the query.

## RejectedReason

Reason why a materialized view was not chosen for a query. For more information, see [Understand why materialized views were rejected](https://cloud.google.com/bigquery/docs/materialized-views-use#understand-rejected) .

Enums

`  REJECTED_REASON_UNSPECIFIED  `

Default unspecified value.

`  NO_DATA  `

View has no cached data because it has not refreshed yet.

`  COST  `

The estimated cost of the view is more expensive than another view or the base table.

Note: The estimate cost might not match the billed cost.

`  BASE_TABLE_TRUNCATED  `

View has no cached data because a base table is truncated.

`  BASE_TABLE_DATA_CHANGE  `

View is invalidated because of a data change in one or more base tables. It could be any recent change if the [`  maxStaleness  `](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#Table.FIELDS.max_staleness) option is not set for the view, or otherwise any change outside of the staleness window.

`  BASE_TABLE_PARTITION_EXPIRATION_CHANGE  `

View is invalidated because a base table's partition expiration has changed.

`  BASE_TABLE_EXPIRED_PARTITION  `

View is invalidated because a base table's partition has expired.

`  BASE_TABLE_INCOMPATIBLE_METADATA_CHANGE  `

View is invalidated because a base table has an incompatible metadata change.

`  TIME_ZONE  `

View is invalidated because it was refreshed with a time zone other than that of the current job.

`  OUT_OF_TIME_TRAVEL_WINDOW  `

View is outside the time travel window.

`  BASE_TABLE_FINE_GRAINED_SECURITY_POLICY  `

View is inaccessible to the user because of a fine-grained security policy on one of its base tables.

`  BASE_TABLE_TOO_STALE  `

One of the view's base tables is too stale. For example, the cached metadata of a BigLake external table needs to be updated.

## MetadataCacheStatistics

Statistics for metadata caching in queried tables.

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
  &quot;tableMetadataCacheUsage&quot;: [
    {
      object (TableMetadataCacheUsage)
    }
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  tableMetadataCacheUsage[]  `

`  object ( TableMetadataCacheUsage  ` )

Set for the Metadata caching eligible tables referenced in the query.

## TableMetadataCacheUsage

Table level detail on the usage of metadata caching. Only set for Metadata caching eligible tables referenced in the query.

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
  &quot;staleness&quot;: string,
  &quot;tableType&quot;: string,
  &quot;tableReference&quot;: {
    object (TableReference)
  },
  &quot;unusedReason&quot;: enum (UnusedReason),
  &quot;explanation&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  staleness  `

`  string ( Duration  ` format)

Duration since last refresh as of this job for managed tables (indicates metadata cache staleness as seen by this job).

A duration in seconds with up to nine fractional digits, ending with ' `  s  ` '. Example: `  "3.5s"  ` .

`  tableType  `

`  string  `

[Table type](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#Table.FIELDS.type) .

`  tableReference  `

`  object ( TableReference  ` )

Metadata caching eligible table referenced in the query.

`  unusedReason  `

`  enum ( UnusedReason  ` )

Reason for not using metadata caching for the table.

`  explanation  `

`  string  `

Free form human-readable reason metadata caching was unused for the job.

## UnusedReason

Reasons for not using metadata caching.

Enums

`  UNUSED_REASON_UNSPECIFIED  `

Unused reasons not specified.

`  EXCEEDED_MAX_STALENESS  `

Metadata cache was outside the table's maxStaleness.

`  METADATA_CACHING_NOT_ENABLED  `

Metadata caching feature is not enabled. [Update BigLake tables](/bigquery/docs/create-cloud-storage-table-biglake#update-biglake-tables) to enable the metadata caching.

`  OTHER_REASON  `

Other unknown reason.

## JobStatistics3

Statistics for a load job.

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
  &quot;inputFiles&quot;: string,
  &quot;inputFileBytes&quot;: string,
  &quot;outputRows&quot;: string,
  &quot;outputBytes&quot;: string,
  &quot;badRecords&quot;: string,
  &quot;timeline&quot;: [
    {
      object (QueryTimelineSample)
    }
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  inputFiles  `

`  string ( Int64Value format)  `

Output only. Number of source files in a load job.

`  inputFileBytes  `

`  string ( Int64Value format)  `

Output only. Number of bytes of source data in a load job.

`  outputRows  `

`  string ( Int64Value format)  `

Output only. Number of rows imported in a load job. Note that while an import job is in the running state, this value may change.

`  outputBytes  `

`  string ( Int64Value format)  `

Output only. Size of the loaded data in bytes. Note that while a load job is in the running state, this value may change.

`  badRecords  `

`  string ( Int64Value format)  `

Output only. The number of bad records encountered. Note that if the job has failed because of more bad records encountered than the maximum allowed in the load job configuration, then this number can be less than the total number of bad records present in the input data.

`  timeline[]  `

`  object ( QueryTimelineSample  ` )

Output only. Describes a timeline of job execution.

## JobStatistics4

Statistics for an extract job.

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
  &quot;destinationUriFileCounts&quot;: [
    string
  ],
  &quot;inputBytes&quot;: string,
  &quot;timeline&quot;: [
    {
      object (QueryTimelineSample)
    }
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  destinationUriFileCounts[]  `

`  string ( int64 format)  `

Output only. Number of files per destination URI or URI pattern specified in the extract configuration. These values will be in the same order as the URIs specified in the 'destinationUris' field.

`  inputBytes  `

`  string ( Int64Value format)  `

Output only. Number of user bytes extracted into the result. This is the byte count as computed by BigQuery for billing purposes and doesn't have any relationship with the number of actual result bytes extracted in the desired format.

`  timeline[]  `

`  object ( QueryTimelineSample  ` )

Output only. Describes a timeline of job execution.

## CopyJobStatistics

Statistics for a copy job.

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
  &quot;copiedRows&quot;: string,
  &quot;copiedLogicalBytes&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  copiedRows  `

`  string ( Int64Value format)  `

Output only. Number of rows copied to the destination table.

`  copiedLogicalBytes  `

`  string ( Int64Value format)  `

Output only. Number of logical bytes copied to the destination table.

## ScriptStatistics

Job statistics specific to the child job of a script.

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
  &quot;evaluationKind&quot;: enum (EvaluationKind),
  &quot;stackFrames&quot;: [
    {
      object (ScriptStackFrame)
    }
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  evaluationKind  `

`  enum ( EvaluationKind  ` )

Whether this child job was a statement or expression.

`  stackFrames[]  `

`  object ( ScriptStackFrame  ` )

Stack trace showing the line/column/procedure name of each frame on the stack at the point where the current evaluation happened. The leaf frame is first, the primary script is last. Never empty.

## EvaluationKind

Describes how the job is evaluated.

Enums

`  EVALUATION_KIND_UNSPECIFIED  `

Default value.

`  STATEMENT  `

The statement appears directly in the script.

`  EXPRESSION  `

The statement evaluates an expression that appears in the script.

## ScriptStackFrame

Represents the location of the statement/expression being evaluated. Line and column numbers are defined as follows:

  - Line and column numbers start with one. That is, line 1 column 1 denotes the start of the script.
  - When inside a stored procedure, all line/column numbers are relative to the procedure body, not the script in which the procedure was defined.
  - Start/end positions exclude leading/trailing comments and whitespace. The end position always ends with a ";", when present.
  - Multi-byte Unicode characters are treated as just one column.
  - If the original script (or procedure definition) contains TAB characters, a tab "snaps" the indentation forward to the nearest multiple of 8 characters, plus 1. For example, a TAB on column 1, 2, 3, 4, 5, 6 , or 8 will advance the next character to column 9. A TAB on column 9, 10, 11, 12, 13, 14, 15, or 16 will advance the next character to column 17.

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
  &quot;startLine&quot;: integer,
  &quot;startColumn&quot;: integer,
  &quot;endLine&quot;: integer,
  &quot;endColumn&quot;: integer,
  &quot;procedureId&quot;: string,
  &quot;text&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  startLine  `

`  integer  `

Output only. One-based start line.

`  startColumn  `

`  integer  `

Output only. One-based start column.

`  endLine  `

`  integer  `

Output only. One-based end line.

`  endColumn  `

`  integer  `

Output only. One-based end column.

`  procedureId  `

`  string  `

Output only. Name of the active procedure, empty if in a top-level script.

`  text  `

`  string  `

Output only. Text of the current statement/expression.

## RowLevelSecurityStatistics

Statistics for row-level security.

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
  &quot;rowLevelSecurityApplied&quot;: boolean
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  rowLevelSecurityApplied  `

`  boolean  `

Whether any accessed data was protected by row access policies.

## DataMaskingStatistics

Statistics for data-masking.

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
  &quot;dataMaskingApplied&quot;: boolean
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  dataMaskingApplied  `

`  boolean  `

Whether any accessed data was protected by the data masking.

## TransactionInfo

\[Alpha\] Information of a multi-statement transaction.

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
  &quot;transactionId&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  transactionId  `

`  string  `

Output only. \[Alpha\] Id of the transaction.

## ReservationEdition

The type of editions. Different features and behaviors are provided to different editions Capacity commitments and reservations are linked to editions.

Enums

`  RESERVATION_EDITION_UNSPECIFIED  `

Default value, which will be treated as ENTERPRISE.

`  STANDARD  `

Standard edition.

`  ENTERPRISE  `

Enterprise edition.

`  ENTERPRISE_PLUS  `

Enterprise Plus edition.

## JobStatus

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
  &quot;errorResult&quot;: {
    object (ErrorProto)
  },
  &quot;errors&quot;: [
    {
      object (ErrorProto)
    }
  ],
  &quot;state&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  errorResult  `

`  object ( ErrorProto  ` )

Output only. Final error result of the job. If present, indicates that the job has completed and was unsuccessful.

`  errors[]  `

`  object ( ErrorProto  ` )

Output only. The first errors encountered during the running of the job. The final message includes the number of errors that caused the process to stop. Errors here do not necessarily mean that the job has not completed or was unsuccessful.

`  state  `

`  string  `

Output only. Running state of the job. Valid states include 'PENDING', 'RUNNING', and 'DONE'.
