---
name: documents/docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job
uri: https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job
title: 'MCP Tools Reference: bigquery.googleapis.com'
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

## Tool: `cancel_job`

Cancel a running BigQuery job.

Use this tool to cancel a query job that is currently executing (i.e. returned `job_complete: false` with a `job_id` from `execute_sql` or `execute_sql_readonly` ). Specify the `job_id` to abort.

The following code sample shows how to use `curl` to call the `cancel_job` MCP tool.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Curl Request</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" data-syntax="Bash" translate="no"><code>curl --location &#39;https://bigquery.googleapis.com/mcp&#39; \
--header &#39;content-type: application/json&#39; \
--header &#39;accept: application/json, text/event-stream&#39; \
--data &#39;{
  &quot;method&quot;: &quot;tools/call&quot;,
  &quot;params&quot;: {
    &quot;name&quot;: &quot;cancel_job&quot;,
    &quot;arguments&quot;: {
      // Provide these details according to the MCP tool specification.
    }
  },
  &quot;jsonrpc&quot;: &quot;2.0&quot;,
  &quot;id&quot;: 1
}&#39;</code></pre></td>
</tr>
</tbody>
</table>

## Input Schema

Request for cancelling a job.

### CancelJobRequest

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;projectId&quot;: string,
  &quot;jobId&quot;: string,
  &quot;location&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`projectId`

`string`

Required. Project ID of the job to cancel.

`jobId`

`string`

Required. Job ID of the job to cancel.

`location`

`string`

Optional. The geographic location of the job.

## Output Schema

Describes format of a jobs cancellation response.

### JobCancelResponse

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;kind&quot;: string,&quot;job&quot;: {object (Job)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`kind`

`string`

The resource type of the response.

`job`

` object ( Job  ` )

The final state of the job.

### Job

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;kind&quot;: string,&quot;etag&quot;: string,&quot;id&quot;: string,&quot;selfLink&quot;: string,&quot;user_email&quot;: string,&quot;configuration&quot;: {object (JobConfiguration)},&quot;jobReference&quot;: {object (JobReference)},&quot;statistics&quot;: {object (JobStatistics)},&quot;status&quot;: {object (JobStatus)},&quot;principal_subject&quot;: string,&quot;jobCreationReason&quot;: {object (JobCreationReason)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`kind`

`string`

Output only. The type of the resource.

`etag`

`string`

Output only. A hash of this resource.

`id`

`string`

Output only. Opaque ID field of the job.

`selfLink`

`string`

Output only. A URL that can be used to access the resource again.

`user_email`

`string`

Output only. Email address of the user who ran the job.

`configuration`

` object ( JobConfiguration  ` )

Required. Describes the job configuration.

`jobReference`

` object ( JobReference  ` )

Optional. Reference describing the unique-per-user name of the job.

`statistics`

` object ( JobStatistics  ` )

Output only. Information about the job, including starting time and ending time of the job.

`status`

` object ( JobStatus  ` )

Output only. The status of this job. Examine this value when polling an asynchronous job to see if the job is complete.

`principal_subject`

`string`

Output only. \[Full-projection-only\] String representation of identity of requesting party. Populated for both first- and third-party identities. Only present for APIs that support third-party identities.

`jobCreationReason`

` object ( JobCreationReason  ` )

Output only. The reason why a Job was created.

### JobConfiguration

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;jobType&quot;: string,&quot;query&quot;: {object (JobConfigurationQuery)},&quot;load&quot;: {object (JobConfigurationLoad)},&quot;copy&quot;: {object (JobConfigurationTableCopy)},&quot;extract&quot;: {object (JobConfigurationExtract)},&quot;dryRun&quot;: boolean,&quot;jobTimeoutMs&quot;: string,&quot;labels&quot;: {string: string,...},// Union field _max_slots can be only one of the following:&quot;maxSlots&quot;: integer// End of list of possible types for union field _max_slots.// Union field _reservation can be only one of the following:&quot;reservation&quot;: string// End of list of possible types for union field _reservation.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`jobType`

`string`

Output only. The type of the job. Can be QUERY, LOAD, EXTRACT, COPY or UNKNOWN.

`query`

` object ( JobConfigurationQuery  ` )

\[Pick one\] Configures a query job.

`load`

` object ( JobConfigurationLoad  ` )

\[Pick one\] Configures a load job.

`copy`

` object ( JobConfigurationTableCopy  ` )

\[Pick one\] Copies a table.

`extract`

` object ( JobConfigurationExtract  ` )

\[Pick one\] Configures an extract job.

`dryRun`

`boolean`

Optional. If set, don't actually run this job. A valid query will return a mostly empty response with some processing statistics, while an invalid query will return the same error it would if it wasn't a dry run. Behavior of non-query jobs is undefined.

`jobTimeoutMs`

`string ( Int64Value format)`

Optional. Job timeout in milliseconds relative to the job creation time. If this time limit is exceeded, BigQuery attempts to stop the job, but might not always succeed in canceling it before the job completes. For example, a job that takes more than 60 seconds to complete has a better chance of being stopped than a job that takes 10 seconds to complete.

`labels`

`map (key: string, value: string)`

The labels associated with this job. You can use these to organize and group your jobs. Label keys and values can be no longer than 63 characters, can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. Label values are optional. Label keys must start with a letter and each label in the list must have a different key.

An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .

Union field `_max_slots` .

`_max_slots` can be only one of the following:

`maxSlots`

`integer`

Optional. A target limit on the rate of slot consumption by this job. If set to a value \> 0, BigQuery will attempt to limit the rate of slot consumption by this job to keep it below the configured limit, even if the job is eligible for more slots based on fair scheduling. The unused slots will be available for other jobs and queries to use.

Note: This feature is not yet generally available.

Union field `_reservation` .

`_reservation` can be only one of the following:

`reservation`

`string`

Optional. The reservation that job would use. User can specify a reservation to execute the job. If reservation is not set, reservation is determined based on the rules defined by the reservation assignments. The expected format is `projects/{project}/locations/{location}/reservations/{reservation}` . Forces the query to use on-demand billing when set to `none` , which requires the project or organization to have `reservation_override_mode` set to `ALLOW_ANY_OVERRIDE` .

### JobConfigurationQuery

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;query&quot;: string,&quot;destinationTable&quot;: {object (TableReference)},&quot;tableDefinitions&quot;: {string: {object (ExternalDataConfiguration)},...},&quot;userDefinedFunctionResources&quot;: [{object (UserDefinedFunctionResource)}],&quot;createDisposition&quot;: string,&quot;writeDisposition&quot;: string,&quot;defaultDataset&quot;: {object (DatasetReference)},&quot;priority&quot;: string,&quot;preserveNulls&quot;: boolean,&quot;allowLargeResults&quot;: boolean,&quot;useQueryCache&quot;: boolean,&quot;flattenResults&quot;: boolean,&quot;maximumBillingTier&quot;: integer,&quot;maximumBytesBilled&quot;: string,&quot;useLegacySql&quot;: boolean,&quot;parameterMode&quot;: string,&quot;queryParameters&quot;: [{object (QueryParameter)}],&quot;schemaUpdateOptions&quot;: [string],&quot;timePartitioning&quot;: {object (TimePartitioning)},&quot;rangePartitioning&quot;: {object (RangePartitioning)},&quot;clustering&quot;: {object (Clustering)},&quot;destinationEncryptionConfiguration&quot;: {object (EncryptionConfiguration)},&quot;scriptOptions&quot;: {object (ScriptOptions)},&quot;connectionProperties&quot;: [{object (ConnectionProperty)}],&quot;createSession&quot;: boolean,&quot;continuous&quot;: boolean,&quot;writeIncrementalResults&quot;: boolean,&quot;secureContext&quot;: {object (SecureContext)},// Union field _system_variables can be only one of the following:&quot;systemVariables&quot;: {object (SystemVariables)}// End of list of possible types for union field _system_variables.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`query`

`string`

\[Required\] SQL query text to execute. The useLegacySql field can be used to indicate whether the query uses legacy SQL or GoogleSQL.

`destinationTable`

` object ( TableReference  ` )

Optional. Describes the table where the query results should be stored. This property must be set for large results that exceed the maximum response size. For queries that produce anonymous (cached) results, this field will be populated by BigQuery.

`tableDefinitions`

` map (key: string, value: object ( ExternalDataConfiguration  ` ))

Optional. You can specify external table definitions, which operate as ephemeral tables that can be queried. These definitions are configured using a JSON map, where the string key represents the table identifier, and the value is the corresponding external data configuration object.

An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .

`userDefinedFunctionResources[]`

` object ( UserDefinedFunctionResource  ` )

Describes user-defined function resources used in the query.

`createDisposition`

`string`

Optional. Specifies whether the job is allowed to create new tables. The following values are supported:

  - CREATE\_IF\_NEEDED: If the table does not exist, BigQuery creates the table.
  - CREATE\_NEVER: The table must already exist. If it does not, a 'notFound' error is returned in the job result.

The default value is CREATE\_IF\_NEEDED. Creation, truncation and append actions occur as one atomic update upon job completion.

`writeDisposition`

`string`

Optional. Specifies the action that occurs if the destination table already exists. The following values are supported:

  - WRITE\_TRUNCATE: If the table already exists, BigQuery overwrites the data, removes the constraints, and uses the schema from the query result.
  - WRITE\_TRUNCATE\_DATA: If the table already exists, BigQuery overwrites the data, but keeps the constraints and schema of the existing table.
  - WRITE\_APPEND: If the table already exists, BigQuery appends the data to the table.
  - WRITE\_EMPTY: If the table already exists and contains data, a 'duplicate' error is returned in the job result.

The default value is WRITE\_EMPTY. Each action is atomic and only occurs if BigQuery is able to complete the job successfully. Creation, truncation and append actions occur as one atomic update upon job completion.

`defaultDataset`

` object ( DatasetReference  ` )

Optional. Specifies the default dataset to use for unqualified table names in the query. This setting does not alter behavior of unqualified dataset names. Setting the system variable `@@dataset_id` achieves the same behavior. See <https://cloud.google.com/bigquery/docs/reference/system-variables> for more information on system variables.

`priority`

`string`

Optional. Specifies a priority for the query. Possible values include INTERACTIVE and BATCH. The default value is INTERACTIVE.

`preserveNulls`

`boolean`

\[Deprecated\] This property is deprecated.

`allowLargeResults`

`boolean`

Optional. If true and query uses legacy SQL dialect, allows the query to produce arbitrarily large result tables at a slight cost in performance. Requires destinationTable to be set. For GoogleSQL queries, this flag is ignored and large results are always allowed. However, you must still set destinationTable when result size exceeds the allowed maximum response size.

`useQueryCache`

`boolean`

Optional. Whether to look for the result in the query cache. The query cache is a best-effort cache that will be flushed whenever tables in the query are modified. Moreover, the query cache is only available when a query does not have a destination table specified. The default value is true.

`flattenResults`

`boolean`

Optional. If true and query uses legacy SQL dialect, flattens all nested and repeated fields in the query results. allowLargeResults must be true if this is set to false. For GoogleSQL queries, this flag is ignored and results are never flattened.

`maximumBillingTier`

`integer`

Optional. \[Deprecated\] Maximum billing tier allowed for this query. The billing tier controls the amount of compute resources allotted to the query, and multiplies the on-demand cost of the query accordingly. A query that runs within its allotted resources will succeed and indicate its billing tier in statistics.query.billingTier, but if the query exceeds its allotted resources, it will fail with billingTierLimitExceeded. WARNING: The billed byte amount can be multiplied by an amount up to this number\! Most users should not need to alter this setting, and we recommend that you avoid introducing new uses of it.

`maximumBytesBilled`

`string ( Int64Value format)`

Limits the bytes billed for this job. Queries that will have bytes billed beyond this limit will fail (without incurring a charge). If unspecified, this will be set to your project default.

`useLegacySql`

`boolean`

Optional. Specifies whether to use BigQuery's legacy SQL dialect for this query. The default value is true. If set to false, the query uses BigQuery's [GoogleSQL](https://docs.cloud.google.com/bigquery/docs/introduction-sql) .

When useLegacySql is set to false, the value of flattenResults is ignored; query will be run as if flattenResults is false.

`parameterMode`

`string`

GoogleSQL only. Set to POSITIONAL to use positional (?) query parameters or to NAMED to use named (@myparam) query parameters in this query.

`queryParameters[]`

` object ( QueryParameter  ` )

Query parameters for GoogleSQL queries.

`schemaUpdateOptions[]`

`string`

Allows the schema of the destination table to be updated as a side effect of the query job. Schema update options are supported in three cases: when writeDisposition is WRITE\_APPEND; when writeDisposition is WRITE\_TRUNCATE\_DATA; when writeDisposition is WRITE\_TRUNCATE and the destination table is a partition of a table, specified by partition decorators. For normal tables, WRITE\_TRUNCATE will always overwrite the schema. One or more of the following values are specified:

  - ALLOW\_FIELD\_ADDITION: allow adding a nullable field to the schema.
  - ALLOW\_FIELD\_RELAXATION: allow relaxing a required field in the original schema to nullable.

`timePartitioning`

` object ( TimePartitioning  ` )

Time-based partitioning specification for the destination table. Only one of timePartitioning and rangePartitioning should be specified.

`rangePartitioning`

` object ( RangePartitioning  ` )

Range partitioning specification for the destination table. Only one of timePartitioning and rangePartitioning should be specified.

`clustering`

` object ( Clustering  ` )

Clustering specification for the destination table.

`destinationEncryptionConfiguration`

` object ( EncryptionConfiguration  ` )

Custom encryption configuration (e.g., Cloud KMS keys)

`scriptOptions`

` object ( ScriptOptions  ` )

Options controlling the execution of scripts.

`connectionProperties[]`

` object ( ConnectionProperty  ` )

Connection properties which can modify the query behavior.

`createSession`

`boolean`

If this property is true, the job creates a new session using a randomly generated session\_id. To continue using a created session with subsequent queries, pass the existing session identifier as a `ConnectionProperty` value. The session identifier is returned as part of the `SessionInfo` message within the query statistics.

The new session's location will be set to `Job.JobReference.location` if it is present, otherwise it's set to the default location based on existing routing logic.

`continuous`

`boolean`

Optional. Whether to run the query as continuous or a regular query. Continuous query is currently in experimental stage and not ready for general usage.

`writeIncrementalResults`

`boolean`

Optional. This is only supported for a SELECT query using a temporary table. If set, the query is allowed to write results incrementally to the temporary result table. This may incur a performance penalty. This option cannot be used with Legacy SQL. This feature is not yet available.

`secureContext`

` object ( SecureContext  ` )

Optional. A set of key-value pairs representing the secure context. This can be used to pass sensitive or context-specific information. They can be retrieved via the SECURE\_CONTEXT() function and used to modify the run-time behavior of a query.

Union field `_system_variables` .

`_system_variables` can be only one of the following:

`systemVariables`

` object ( SystemVariables  ` )

Output only. System variables for GoogleSQL queries. A system variable is output if the variable is settable and its value differs from the system default. "@@" prefix is not included in the name of the System variables.

### TableReference

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;projectId&quot;: string,
  &quot;datasetId&quot;: string,
  &quot;tableId&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`projectId`

`string`

Required. The ID of the project containing this table.

`datasetId`

`string`

Required. The ID of the dataset containing this table.

`tableId`

`string`

Required. The ID of the table. The ID can contain Unicode characters in category L (letter), M (mark), N (number), Pc (connector, including underscore), Pd (dash), and Zs (space). For more information, see [General Category](https://wikipedia.org/wiki/Unicode_character_property#General_Category) . The maximum length is 1,024 characters. Certain operations allow suffixing of the table ID with a partition decorator, such as `sample_table$20190123` .

### ExternalTableDefinitionsEntry

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;key&quot;: string,&quot;value&quot;: {object (ExternalDataConfiguration)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`key`

`string`

`value`

` object ( ExternalDataConfiguration  ` )

### ExternalDataConfiguration

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;sourceUris&quot;: [string],&quot;fileSetSpecType&quot;: enum (FileSetSpecType),&quot;schema&quot;: {object (TableSchema)},&quot;sourceFormat&quot;: string,&quot;maxBadRecords&quot;: integer,&quot;autodetect&quot;: boolean,&quot;ignoreUnknownValues&quot;: boolean,&quot;compression&quot;: string,&quot;csvOptions&quot;: {object (CsvOptions)},&quot;jsonOptions&quot;: {object (JsonOptions)},&quot;bigtableOptions&quot;: {object (BigtableOptions)},&quot;googleSheetsOptions&quot;: {object (GoogleSheetsOptions)},&quot;hivePartitioningOptions&quot;: {object (HivePartitioningOptions)},&quot;connectionId&quot;: string,&quot;decimalTargetTypes&quot;: [enum (DecimalTargetType)],&quot;avroOptions&quot;: {object (AvroOptions)},&quot;jsonExtension&quot;: enum (JsonExtension),&quot;parquetOptions&quot;: {object (ParquetOptions)},&quot;referenceFileSchemaUri&quot;: string,&quot;metadataCacheMode&quot;: enum (MetadataCacheMode),&quot;timestampTargetPrecision&quot;: [integer],// Union field _object_metadata can be only one of the following:&quot;objectMetadata&quot;: enum (ObjectMetadata)// End of list of possible types for union field _object_metadata.// Union field _time_zone can be only one of the following:&quot;timeZone&quot;: string// End of list of possible types for union field _time_zone.// Union field _date_format can be only one of the following:&quot;dateFormat&quot;: string// End of list of possible types for union field _date_format.// Union field _datetime_format can be only one of the following:&quot;datetimeFormat&quot;: string// End of list of possible types for union field _datetime_format.// Union field _time_format can be only one of the following:&quot;timeFormat&quot;: string// End of list of possible types for union field _time_format.// Union field _timestamp_format can be only one of the following:&quot;timestampFormat&quot;: string// End of list of possible types for union field _timestamp_format.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`sourceUris[]`

`string`

\[Required\] The fully-qualified URIs that point to your data in Google Cloud. For Google Cloud Storage URIs: Each URI can contain one '\*' wildcard character and it must come after the 'bucket' name. Size limits related to load jobs apply to external data sources. For Google Cloud Bigtable URIs: Exactly one URI can be specified and it has be a fully specified and valid HTTPS URL for a Google Cloud Bigtable table. For Google Cloud Datastore backups, exactly one URI can be specified. Also, the '\*' wildcard character is not allowed.

`fileSetSpecType`

` enum ( FileSetSpecType  ` )

Optional. Specifies how source URIs are interpreted for constructing the file set to load. By default source URIs are expanded against the underlying storage. Other options include specifying manifest files. Only applicable to object storage systems.

`schema`

` object ( TableSchema  ` )

Optional. The schema for the data. Schema is required for CSV and JSON formats if autodetect is not on. Schema is disallowed for Google Cloud Bigtable, Cloud Datastore backups, Avro, ORC and Parquet formats.

`sourceFormat`

`string`

\[Required\] The data format. For CSV files, specify "CSV". For Google sheets, specify "GOOGLE\_SHEETS". For newline-delimited JSON, specify "NEWLINE\_DELIMITED\_JSON". For Avro files, specify "AVRO". For Google Cloud Datastore backups, specify "DATASTORE\_BACKUP". For Apache Iceberg tables, specify "ICEBERG". For ORC files, specify "ORC". For Parquet files, specify "PARQUET". \[Beta\] For Google Cloud Bigtable, specify "BIGTABLE".

`maxBadRecords`

`integer`

Optional. The maximum number of bad records that BigQuery can ignore when reading data. If the number of bad records exceeds this value, an invalid error is returned in the job result. The default value is 0, which requires that all records are valid. This setting is ignored for Google Cloud Bigtable, Google Cloud Datastore backups, Avro, ORC and Parquet formats.

`autodetect`

`boolean`

Try to detect schema and format options automatically. Any option specified explicitly will be honored.

`ignoreUnknownValues`

`boolean`

Optional. Indicates if BigQuery should allow extra values that are not represented in the table schema. If true, the extra values are ignored. If false, records with extra columns are treated as bad records, and if there are too many bad records, an invalid error is returned in the job result. The default value is false. The sourceFormat property determines what BigQuery treats as an extra value: CSV: Trailing columns JSON: Named values that don't match any column names Google Cloud Bigtable: This setting is ignored. Google Cloud Datastore backups: This setting is ignored. Avro: This setting is ignored. ORC: This setting is ignored. Parquet: This setting is ignored.

`compression`

`string`

Optional. The compression type of the data source. Possible values include GZIP and NONE. The default value is NONE. This setting is ignored for Google Cloud Bigtable, Google Cloud Datastore backups, Avro, ORC and Parquet formats. An empty string is an invalid value.

`csvOptions`

` object ( CsvOptions  ` )

Optional. Additional properties to set if sourceFormat is set to CSV.

`jsonOptions`

` object ( JsonOptions  ` )

Optional. Additional properties to set if sourceFormat is set to JSON.

`bigtableOptions`

` object ( BigtableOptions  ` )

Optional. Additional options if sourceFormat is set to BIGTABLE.

`googleSheetsOptions`

` object ( GoogleSheetsOptions  ` )

Optional. Additional options if sourceFormat is set to GOOGLE\_SHEETS.

`hivePartitioningOptions`

` object ( HivePartitioningOptions  ` )

Optional. When set, configures hive partitioning support. Not all storage formats support hive partitioning -- requesting hive partitioning on an unsupported format will lead to an error, as will providing an invalid specification.

`connectionId`

`string`

Optional. The connection specifying the credentials to be used to read external storage, such as Azure Blob, Cloud Storage, or S3. The connection\_id can have the form `{project_id}.{location_id};{connection_id}` or `projects/{project_id}/locations/{location_id}/connections/{connection_id}` .

`decimalTargetTypes[]`

` enum ( DecimalTargetType  ` )

Defines the list of possible SQL data types to which the source decimal values are converted. This list and the precision and the scale parameters of the decimal field determine the target type. In the order of NUMERIC, BIGNUMERIC, and STRING, a type is picked if it is in the specified list and if it supports the precision and the scale. STRING supports all precision and scale values. If none of the listed types supports the precision and the scale, the type supporting the widest range in the specified list is picked, and if a value exceeds the supported range when reading the data, an error will be thrown.

Example: Suppose the value of this field is \["NUMERIC", "BIGNUMERIC"\]. If (precision,scale) is:

  - (38,9) -\> NUMERIC;
  - (39,9) -\> BIGNUMERIC (NUMERIC cannot hold 30 integer digits);
  - (38,10) -\> BIGNUMERIC (NUMERIC cannot hold 10 fractional digits);
  - (76,38) -\> BIGNUMERIC;
  - (77,38) -\> BIGNUMERIC (error if value exceeds supported range).

This field cannot contain duplicate types. The order of the types in this field is ignored. For example, \["BIGNUMERIC", "NUMERIC"\] is the same as \["NUMERIC", "BIGNUMERIC"\] and NUMERIC always takes precedence over BIGNUMERIC.

Defaults to \["NUMERIC", "STRING"\] for ORC and \["NUMERIC"\] for the other file formats.

`avroOptions`

` object ( AvroOptions  ` )

Optional. Additional properties to set if sourceFormat is set to AVRO.

`jsonExtension`

` enum ( JsonExtension  ` )

Optional. Load option to be used together with source\_format newline-delimited JSON to indicate that a variant of JSON is being loaded. To load newline-delimited GeoJSON, specify GEOJSON (and source\_format must be set to NEWLINE\_DELIMITED\_JSON).

`parquetOptions`

` object ( ParquetOptions  ` )

Optional. Additional properties to set if sourceFormat is set to PARQUET.

`referenceFileSchemaUri`

`string`

Optional. When creating an external table, the user can provide a reference file with the table schema. This is enabled for the following formats: AVRO, PARQUET, ORC.

`metadataCacheMode`

` enum ( MetadataCacheMode  ` )

Optional. Metadata Cache Mode for the table. Set this to enable caching of metadata from external data source.

`timestampTargetPrecision[]`

`integer`

Precisions (maximum number of total digits in base 10) for seconds of TIMESTAMP types that are allowed to the destination table for autodetection mode.

Available for the formats: CSV, PARQUET, AVRO, and Iceberg External Table.

Possible values include: Not Specified, \[\], or \[6\]: timestamp(6) for all auto detected TIMESTAMP columns \[6, 12\]: timestamp(6) for all auto detected TIMESTAMP columns that have less than 6 digits of subseconds. timestamp(12) for all auto detected TIMESTAMP columns that have more than 6 digits of subseconds. \[12\]: timestamp(12) for all auto detected TIMESTAMP columns.

The order of the elements in this array is ignored. Inputs that have higher precision than the highest target precision in this array will be truncated.

Union field `_object_metadata` .

`_object_metadata` can be only one of the following:

`objectMetadata`

` enum ( ObjectMetadata  ` )

Optional. ObjectMetadata is used to create Object Tables. Object Tables contain a listing of objects (with their metadata) found at the source\_uris. If ObjectMetadata is set, source\_format should be omitted.

Currently SIMPLE is the only supported Object Metadata type.

Union field `_time_zone` .

`_time_zone` can be only one of the following:

`timeZone`

`string`

Optional. Time zone used when parsing timestamp values that do not have specific time zone information (e.g. 2024-04-20 12:34:56). The expected format is a IANA timezone string (e.g. America/Los\_Angeles).

Union field `_date_format` .

`_date_format` can be only one of the following:

`dateFormat`

`string`

Optional. Format used to parse DATE values. Supports C-style and SQL-style values.

Union field `_datetime_format` .

`_datetime_format` can be only one of the following:

`datetimeFormat`

`string`

Optional. Format used to parse DATETIME values. Supports C-style and SQL-style values.

Union field `_time_format` .

`_time_format` can be only one of the following:

`timeFormat`

`string`

Optional. Format used to parse TIME values. Supports C-style and SQL-style values.

Union field `_timestamp_format` .

`_timestamp_format` can be only one of the following:

`timestampFormat`

`string`

Optional. Format used to parse TIMESTAMP values. Supports C-style and SQL-style values.

### TableSchema

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;fields&quot;: [{object (TableFieldSchema)}],&quot;foreignTypeInfo&quot;: {object (ForeignTypeInfo)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`fields[]`

` object ( TableFieldSchema  ` )

Describes the fields in a table.

`foreignTypeInfo`

` object ( ForeignTypeInfo  ` )

Optional. Specifies metadata of the foreign data type definition in field schema ( `TableFieldSchema.foreign_type_definition` ).

### TableFieldSchema

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;type&quot;: string,&quot;mode&quot;: string,&quot;fields&quot;: [{object (TableFieldSchema)}],&quot;description&quot;: string,&quot;policyTags&quot;: {object (PolicyTagList)},&quot;dataGovernanceTagsInfo&quot;: {object (DataGovernanceTagsInfo)},&quot;dataPolicies&quot;: [{object (DataPolicyOption)}],&quot;dataPolicyList&quot;: {object (DataPolicyList)},&quot;maxLength&quot;: string,&quot;precision&quot;: string,&quot;scale&quot;: string,&quot;timestampPrecision&quot;: string,&quot;roundingMode&quot;: enum (RoundingMode),&quot;collation&quot;: string,&quot;defaultValueExpression&quot;: string,&quot;rangeElementType&quot;: {object (FieldElementType)},&quot;foreignTypeDefinition&quot;: string,&quot;generatedColumn&quot;: {object (GeneratedColumn)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`name`

`string`

Required. The field name. The name must contain only letters (a-z, A-Z), numbers (0-9), or underscores (\_), and must start with a letter or underscore. The maximum length is 300 characters.

`type`

`string`

Required. The field data type. Possible values include:

  - STRING
  - BYTES
  - INTEGER (or INT64)
  - FLOAT (or FLOAT64)
  - BOOLEAN (or BOOL)
  - TIMESTAMP
  - DATE
  - TIME
  - DATETIME
  - GEOGRAPHY
  - NUMERIC
  - BIGNUMERIC
  - JSON
  - RECORD (or STRUCT)
  - RANGE

Use of RECORD/STRUCT indicates that the field contains a nested schema.

`mode`

`string`

Optional. The field mode. Possible values include NULLABLE, REQUIRED and REPEATED. The default value is NULLABLE.

`fields[]`

` object ( TableFieldSchema  ` )

Optional. Describes the nested schema fields if the type property is set to RECORD.

`description`

`string`

Optional. The field description. The maximum length is 1,024 characters.

`policyTags`

` object ( PolicyTagList  ` )

Optional. The policy tags attached to this field, used for field-level access control. If not set, defaults to empty policy\_tags.

`dataGovernanceTagsInfo`

` object ( DataGovernanceTagsInfo  ` )

Optional. Specifies the data governance tags on this field. This field works with other column-level security fields as follows:

  - **Precedence** : If a data governance tag is attached to a column, it takes precedence over the policy tag attached to the column. However, if a data policy is attached to a column, it takes precedence over the data governance tag.
  - **Patching behavior** : Describes how this field behaves during a `Table.patch` schema update:
      - **Unset** : If the `data_governance_tags_info` field is omitted from the update request, the existing tags on the column are preserved.
      - **Empty Field** : To clear data governance tags from a column, send the `data_governance_tags_info` field as an empty object. This removes all tags from the column.
      - **Updating tags** : To replace an existing tag, send the field with the new tag.

`dataPolicies[]`

` object ( DataPolicyOption  ` )

Optional. Data policies attached to this field, used for field-level access control.

`dataPolicyList`

` object ( DataPolicyList  ` )

Optional. Specifies data policies attached to this field, used for field-level access control. When set, this will be the source of truth for data policy information.

`maxLength`

`string ( int64 format)`

Optional. Maximum length of values of this field for STRINGS or BYTES.

If max\_length is not specified, no maximum length constraint is imposed on this field.

If type = "STRING", then max\_length represents the maximum UTF-8 length of strings in this field.

If type = "BYTES", then max\_length represents the maximum number of bytes in this field.

It is invalid to set this field if type ≠ "STRING" and ≠ "BYTES".

`precision`

`string ( int64 format)`

Optional. Precision (maximum number of total digits in base 10) and scale (maximum number of digits in the fractional part in base 10) constraints for values of this field for NUMERIC or BIGNUMERIC.

It is invalid to set precision or scale if type ≠ "NUMERIC" and ≠ "BIGNUMERIC".

If precision and scale are not specified, no value range constraint is imposed on this field insofar as values are permitted by the type.

Values of this NUMERIC or BIGNUMERIC field must be in this range when:

  - Precision ( P ) and scale ( S ) are specified: \[-10 <sup>P - S</sup> + 10 <sup>- S</sup> , 10 <sup>P - S</sup> - 10 <sup>- S</sup> \]
  - Precision ( P ) is specified but not scale (and thus scale is interpreted to be equal to zero): \[-10 <sup>P</sup> + 1, 10 <sup>P</sup> - 1\].

Acceptable values for precision and scale if both are specified:

  - If type = "NUMERIC": 1 ≤ precision - scale ≤ 29 and 0 ≤ scale ≤ 9.
  - If type = "BIGNUMERIC": 1 ≤ precision - scale ≤ 38 and 0 ≤ scale ≤ 38.

Acceptable values for precision if only precision is specified but not scale (and thus scale is interpreted to be equal to zero):

  - If type = "NUMERIC": 1 ≤ precision ≤ 29.
  - If type = "BIGNUMERIC": 1 ≤ precision ≤ 38.

If scale is specified but not precision, then it is invalid.

`scale`

`string ( int64 format)`

Optional. See documentation for precision.

`timestampPrecision`

`string ( Int64Value format)`

Optional. Precision (maximum number of total digits in base 10) for seconds of TIMESTAMP type.

Possible values include: \* 6 (Default, for TIMESTAMP type with microsecond precision) \* 12 (For TIMESTAMP type with picosecond precision)

`roundingMode`

` enum ( RoundingMode  ` )

Optional. Specifies the rounding mode to be used when storing values of NUMERIC and BIGNUMERIC type.

`collation`

`string`

Optional. Field collation can be set only when the type of field is STRING. The following values are supported:

  - 'und:ci': undetermined locale, case insensitive.
  - '': empty string. Default to case-sensitive behavior.

`defaultValueExpression`

`string`

Optional. A SQL expression to specify the [default value](https://cloud.google.com/bigquery/docs/default-values) for this field.

`rangeElementType`

` object ( FieldElementType  ` )

Optional. The subtype of the RANGE, if the type of this field is RANGE. If the type is RANGE, this field is required. Values for the field element type can be the following:

  - DATE
  - DATETIME
  - TIMESTAMP

`foreignTypeDefinition`

`string`

Optional. Definition of the foreign data type. Only valid for top-level schema fields (not nested fields). If the type is FOREIGN, this field is required.

`generatedColumn`

` object ( GeneratedColumn  ` )

Optional. Definition of how values are generated for the field. Only valid for top-level schema fields (not nested fields).

### StringValue

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;value&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`value`

`string`

The string value.

### PolicyTagList

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;names&quot;: [
    string
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`names[]`

`string`

A list of policy tag resource names. For example, "projects/1/locations/eu/taxonomies/2/policyTags/3". At most 1 policy tag is currently allowed.

### DataGovernanceTagsInfo

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;dataGovernanceTags&quot;: {
    string: string,
    ...
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`dataGovernanceTags`

`map (key: string, value: string)`

Optional. The data governance tags added to this field are used for field-level access control. Only one data governance tag is currently supported on a field. Tag keys are globally unique. Tag key is expected to be in the namespaced format, for example "parent-id/pii" where parent-id is the ID of the parent organization or project resource for this tag key. Tag value is expected to be the short name, for example "sensitive". See [Tag definitions](https://cloud.google.com/iam/docs/tags-access-control#definitions) for more details. For example: "parent-id/pii": "sensitive", "myProject/cost\_center": "sales"

An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .

### DataGovernanceTagsEntry

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;key&quot;: string,
  &quot;value&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`key`

`string`

`value`

`string`

### DataPolicyOption

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _name can be only one of the following:&quot;name&quot;: string// End of list of possible types for union field _name.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_name` .

`_name` can be only one of the following:

`name`

`string`

Data policy resource name in the form of projects/project\_id/locations/location\_id/dataPolicies/data\_policy\_id.

### DataPolicyList

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;dataPolicies&quot;: [{object (DataPolicyOption)}]}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`dataPolicies[]`

` object ( DataPolicyOption  ` )

Contains a list of data policy options. At most 9 data policies are allowed per field.

### Int64Value

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;value&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`value`

`string ( int64 format)`

The int64 value.

### FieldElementType

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;type&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`type`

`string`

Required. The type of a field element. For more information, see `TableFieldSchema.type` .

### GeneratedColumn

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _generated_mode can be only one of the following:&quot;generatedMode&quot;: enum (GeneratedMode)// End of list of possible types for union field _generated_mode.// Union field definition can be only one of the following:&quot;generatedExpressionInfo&quot;: {object (GeneratedExpressionInfo)}// End of list of possible types for union field definition.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_generated_mode` .

`_generated_mode` can be only one of the following:

`generatedMode`

` enum ( GeneratedMode  ` )

Optional. Dictates when system generated values are used to populate the field.

Union field `definition` .

`definition` can be only one of the following:

`generatedExpressionInfo`

` object ( GeneratedExpressionInfo  ` )

Definition of the expression used to generate the field.

### GeneratedExpressionInfo

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _generation_expression can be only one of the following:&quot;generationExpression&quot;: string// End of list of possible types for union field _generation_expression.// Union field _asynchronous can be only one of the following:&quot;asynchronous&quot;: boolean// End of list of possible types for union field _asynchronous.// Union field _stored can be only one of the following:&quot;stored&quot;: boolean// End of list of possible types for union field _stored.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_generation_expression` .

`_generation_expression` can be only one of the following:

`generationExpression`

`string`

Optional. The generation expression (e.g. AI.EMBED(...)) used to generate the field.

Union field `_asynchronous` .

`_asynchronous` can be only one of the following:

`asynchronous`

`boolean`

Optional. Whether the column generation is done asynchronously.

Union field `_stored` .

`_stored` can be only one of the following:

`stored`

`boolean`

Optional. Whether the generated column is stored in the table.

### ForeignTypeInfo

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;typeSystem&quot;: enum (TypeSystem)}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`typeSystem`

` enum ( TypeSystem  ` )

Required. Specifies the system which defines the foreign data type.

### Int32Value

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;value&quot;: integer
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`value`

`integer`

The int32 value.

### BoolValue

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;value&quot;: boolean
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`value`

`boolean`

The bool value.

### CsvOptions

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;fieldDelimiter&quot;: string,
  &quot;skipLeadingRows&quot;: string,
  &quot;quote&quot;: string,
  &quot;allowQuotedNewlines&quot;: boolean,
  &quot;allowJaggedRows&quot;: boolean,
  &quot;encoding&quot;: string,
  &quot;preserveAsciiControlCharacters&quot;: boolean,
  &quot;nullMarker&quot;: string,
  &quot;nullMarkers&quot;: [
    string
  ],
  &quot;sourceColumnMatch&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`fieldDelimiter`

`string`

Optional. The separator character for fields in a CSV file. The separator is interpreted as a single byte. For files encoded in ISO-8859-1, any single character can be used as a separator. For files encoded in UTF-8, characters represented in decimal range 1-127 (U+0001-U+007F) can be used without any modification. UTF-8 characters encoded with multiple bytes (i.e. U+0080 and above) will have only the first byte used for separating fields. The remaining bytes will be treated as a part of the field. BigQuery also supports the escape sequence "\\t" (U+0009) to specify a tab separator. The default value is comma (",", U+002C).

`skipLeadingRows`

`string ( Int64Value format)`

Optional. The number of rows at the top of a CSV file that BigQuery will skip when reading the data. The default value is 0. This property is useful if you have header rows in the file that should be skipped. When autodetect is on, the behavior is the following:

  - skipLeadingRows unspecified - Autodetect tries to detect headers in the first row. If they are not detected, the row is read as data. Otherwise data is read starting from the second row.
  - skipLeadingRows is 0 - Instructs autodetect that there are no headers and data should be read starting from the first row.
  - skipLeadingRows = N \> 0 - Autodetect skips N-1 rows and tries to detect headers in row N. If headers are not detected, row N is just skipped. Otherwise row N is used to extract column names for the detected schema.

`quote`

`string`

Optional. The value that is used to quote data sections in a CSV file. BigQuery converts the string to ISO-8859-1 encoding, and then uses the first byte of the encoded string to split the data in its raw, binary state. The default value is a double-quote ("). If your data does not contain quoted sections, set the property value to an empty string. If your data contains quoted newline characters, you must also set the allowQuotedNewlines property to true. To include the specific quote character within a quoted value, precede it with an additional matching quote character. For example, if you want to escape the default character ' " ', use ' "" '.

`allowQuotedNewlines`

`boolean`

Optional. Indicates if BigQuery should allow quoted data sections that contain newline characters in a CSV file. The default value is false.

`allowJaggedRows`

`boolean`

Optional. Indicates if BigQuery should accept rows that are missing trailing optional columns. If true, BigQuery treats missing trailing columns as null values. If false, records with missing trailing columns are treated as bad records, and if there are too many bad records, an invalid error is returned in the job result. The default value is false.

`encoding`

`string`

Optional. The character encoding of the data. The supported values are UTF-8, ISO-8859-1, UTF-16BE, UTF-16LE, UTF-32BE, and UTF-32LE. The default value is UTF-8. BigQuery decodes the data after the raw, binary data has been split using the values of the quote and fieldDelimiter properties.

`preserveAsciiControlCharacters`

`boolean`

Optional. Indicates if the embedded ASCII control characters (the first 32 characters in the ASCII-table, from '\\x00' to '\\x1F') are preserved.

`nullMarker`

`string`

Optional. Specifies a string that represents a null value in a CSV file. For example, if you specify "\\N", BigQuery interprets "\\N" as a null value when querying a CSV file. The default value is the empty string. If you set this property to a custom value, BigQuery throws an error if an empty string is present for all data types except for STRING and BYTE. For STRING and BYTE columns, BigQuery interprets the empty string as an empty value.

`nullMarkers[]`

`string`

Optional. A list of strings represented as SQL NULL value in a CSV file.

null\_marker and null\_markers can't be set at the same time. If null\_marker is set, null\_markers has to be not set. If null\_markers is set, null\_marker has to be not set. If both null\_marker and null\_markers are set at the same time, a user error would be thrown. Any strings listed in null\_markers, including empty string would be interpreted as SQL NULL. This applies to all column types.

`sourceColumnMatch`

`string`

Optional. Controls the strategy used to match loaded columns to the schema. If not set, a sensible default is chosen based on how the schema is provided. If autodetect is used, then columns are matched by name. Otherwise, columns are matched by position. This is done to keep the behavior backward-compatible. Acceptable values are: POSITION - matches by position. This assumes that the columns are ordered the same way as the schema. NAME - matches by name. This reads the header row as column names and reorders columns to match the field names in the schema.

### JsonOptions

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;encoding&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`encoding`

`string`

Optional. The character encoding of the data. The supported values are UTF-8, UTF-16BE, UTF-16LE, UTF-32BE, and UTF-32LE. The default value is UTF-8.

### BigtableOptions

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;columnFamilies&quot;: [{object (BigtableColumnFamily)}],&quot;ignoreUnspecifiedColumnFamilies&quot;: boolean,&quot;readRowkeyAsString&quot;: boolean,&quot;outputColumnFamiliesAsJson&quot;: boolean}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`columnFamilies[]`

` object ( BigtableColumnFamily  ` )

Optional. List of column families to expose in the table schema along with their types. This list restricts the column families that can be referenced in queries and specifies their value types. You can use this list to do type conversions - see the 'type' field for more details. If you leave this list empty, all column families are present in the table schema and their values are read as BYTES. During a query only the column families referenced in that query are read from Bigtable.

`ignoreUnspecifiedColumnFamilies`

`boolean`

Optional. If field is true, then the column families that are not specified in columnFamilies list are not exposed in the table schema. Otherwise, they are read with BYTES type values. The default value is false.

`readRowkeyAsString`

`boolean`

Optional. If field is true, then the rowkey column families will be read and converted to string. Otherwise they are read with BYTES type values and users need to manually cast them with CAST if necessary. The default value is false.

`outputColumnFamiliesAsJson`

`boolean`

Optional. If field is true, then each column family will be read as a single JSON column. Otherwise they are read as a repeated cell structure containing timestamp/value tuples. The default value is false.

### BigtableColumnFamily

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;familyId&quot;: string,&quot;type&quot;: string,&quot;encoding&quot;: string,&quot;columns&quot;: [{object (BigtableColumn)}],&quot;onlyReadLatest&quot;: boolean,&quot;protoConfig&quot;: {object (BigtableProtoConfig)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`familyId`

`string`

Identifier of the column family.

`type`

`string`

Optional. The type to convert the value in cells of this column family. The values are expected to be encoded using HBase Bytes.toBytes function when using the BINARY encoding value. Following BigQuery types are allowed (case-sensitive):

  - BYTES
  - STRING
  - INTEGER
  - FLOAT
  - BOOLEAN
  - JSON

Default type is BYTES. This can be overridden for a specific column by listing that column in 'columns' and specifying a type for it.

`encoding`

`string`

Optional. The encoding of the values when the type is not STRING. Acceptable encoding values are: TEXT - indicates values are alphanumeric text strings. BINARY - indicates values are encoded using HBase Bytes.toBytes family of functions. PROTO\_BINARY - indicates values are encoded using serialized proto messages. This can only be used in combination with JSON type. This can be overridden for a specific column by listing that column in 'columns' and specifying an encoding for it.

`columns[]`

` object ( BigtableColumn  ` )

Optional. Lists of columns that should be exposed as individual fields as opposed to a list of (column name, value) pairs. All columns whose qualifier matches a qualifier in this list can be accessed as `<family field name>.<column field name>` . Other columns can be accessed as a list through the `<family field name>.Column` field.

`onlyReadLatest`

`boolean`

Optional. If this is set only the latest version of value are exposed for all columns in this column family. This can be overridden for a specific column by listing that column in 'columns' and specifying a different setting for that column.

`protoConfig`

` object ( BigtableProtoConfig  ` )

Optional. Protobuf-specific configurations, only takes effect when the encoding is PROTO\_BINARY.

### BigtableColumn

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;qualifierEncoded&quot;: string,&quot;qualifierString&quot;: string,&quot;fieldName&quot;: string,&quot;type&quot;: string,&quot;encoding&quot;: string,&quot;onlyReadLatest&quot;: boolean,&quot;protoConfig&quot;: {object (BigtableProtoConfig)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`qualifierEncoded`

`string ( BytesValue format)`

\[Required\] Qualifier of the column. Columns in the parent column family that has this exact qualifier are exposed as `<family field name>.<column field name>` field. If the qualifier is valid UTF-8 string, it can be specified in the qualifier\_string field. Otherwise, a base-64 encoded value must be set to qualifier\_encoded. The column field name is the same as the column qualifier. However, if the qualifier is not a valid BigQuery field identifier i.e. does not match \[a-zA-Z\]\[a-zA-Z0-9\_\]\*, a valid identifier must be provided as field\_name.

`qualifierString`

`string`

Qualifier string.

`fieldName`

`string`

Optional. If the qualifier is not a valid BigQuery field identifier i.e. does not match \[a-zA-Z\]\[a-zA-Z0-9\_\]\*, a valid identifier must be provided as the column field name and is used as field name in queries.

`type`

`string`

Optional. The type to convert the value in cells of this column. The values are expected to be encoded using HBase Bytes.toBytes function when using the BINARY encoding value. Following BigQuery types are allowed (case-sensitive):

  - BYTES
  - STRING
  - INTEGER
  - FLOAT
  - BOOLEAN
  - JSON

Default type is BYTES. 'type' can also be set at the column family level. However, the setting at this level takes precedence if 'type' is set at both levels.

`encoding`

`string`

Optional. The encoding of the values when the type is not STRING. Acceptable encoding values are: TEXT - indicates values are alphanumeric text strings. BINARY - indicates values are encoded using HBase Bytes.toBytes family of functions. PROTO\_BINARY - indicates values are encoded using serialized proto messages. This can only be used in combination with JSON type. 'encoding' can also be set at the column family level. However, the setting at this level takes precedence if 'encoding' is set at both levels.

`onlyReadLatest`

`boolean`

Optional. If this is set, only the latest version of value in this column are exposed. 'onlyReadLatest' can also be set at the column family level. However, the setting at this level takes precedence if 'onlyReadLatest' is set at both levels.

`protoConfig`

` object ( BigtableProtoConfig  ` )

Optional. Protobuf-specific configurations, only takes effect when the encoding is PROTO\_BINARY.

### BytesValue

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;value&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`value`

`string ( bytes format)`

The bytes value.

A base64-encoded string.

### BigtableProtoConfig

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;schemaBundleId&quot;: string,
  &quot;protoMessageName&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`schemaBundleId`

`string`

Optional. The ID of the Bigtable SchemaBundle resource associated with this protobuf. The ID should be referred to within the parent table, e.g., `foo` rather than `projects/{project}/instances/{instance}/tables/{table}/schemaBundles/foo` . See [more details on Bigtable SchemaBundles](https://docs.cloud.google.com/bigtable/docs/create-manage-protobuf-schemas) .

`protoMessageName`

`string`

Optional. The fully qualified proto message name of the protobuf. In the format of "foo.bar.Message".

### GoogleSheetsOptions

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;skipLeadingRows&quot;: string,
  &quot;range&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`skipLeadingRows`

`string ( Int64Value format)`

Optional. The number of rows at the top of a sheet that BigQuery will skip when reading the data. The default value is 0. This property is useful if you have header rows that should be skipped. When autodetect is on, the behavior is the following: \* skipLeadingRows unspecified - Autodetect tries to detect headers in the first row. If they are not detected, the row is read as data. Otherwise data is read starting from the second row. \* skipLeadingRows is 0 - Instructs autodetect that there are no headers and data should be read starting from the first row. \* skipLeadingRows = N \> 0 - Autodetect skips N-1 rows and tries to detect headers in row N. If headers are not detected, row N is just skipped. Otherwise row N is used to extract column names for the detected schema.

`range`

`string`

Optional. Range of a sheet to query from. Only used when non-empty. Typical format: sheet\_name\!top\_left\_cell\_id:bottom\_right\_cell\_id For example: sheet1\!A1:B20

### HivePartitioningOptions

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;mode&quot;: string,
  &quot;sourceUriPrefix&quot;: string,
  &quot;requirePartitionFilter&quot;: boolean,
  &quot;fields&quot;: [
    string
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`mode`

`string`

Optional. When set, what mode of hive partitioning to use when reading data. The following modes are supported:

  - AUTO: automatically infer partition key name(s) and type(s).

  - STRINGS: automatically infer partition key name(s). All types are strings.

  - CUSTOM: partition key schema is encoded in the source URI prefix.

Not all storage formats support hive partitioning. Requesting hive partitioning on an unsupported format will lead to an error. Currently supported formats are: JSON, CSV, ORC, Avro and Parquet.

`sourceUriPrefix`

`string`

Optional. When hive partition detection is requested, a common prefix for all source uris must be required. The prefix must end immediately before the partition key encoding begins. For example, consider files following this data layout:

gs://bucket/path\_to\_table/dt=2019-06-01/country=USA/id=7/file.avro

gs://bucket/path\_to\_table/dt=2019-05-31/country=CA/id=3/file.avro

When hive partitioning is requested with either AUTO or STRINGS detection, the common prefix can be either of gs://bucket/path\_to\_table or gs://bucket/path\_to\_table/.

CUSTOM detection requires encoding the partitioning schema immediately after the common prefix. For CUSTOM, any of

  - gs://bucket/path\_to\_table/{dt:DATE}/{country:STRING}/{id:INTEGER}

  - gs://bucket/path\_to\_table/{dt:STRING}/{country:STRING}/{id:INTEGER}

  - gs://bucket/path\_to\_table/{dt:DATE}/{country:STRING}/{id:STRING}

would all be valid source URI prefixes.

`requirePartitionFilter`

`boolean`

Optional. If set to true, queries over this table require a partition filter that can be used for partition elimination to be specified.

Note that this field should only be true when creating a permanent external table or querying a temporary external table.

Hive-partitioned loads with require\_partition\_filter explicitly set to true will fail.

`fields[]`

`string`

Output only. For permanent external tables, this field is populated with the hive partition keys in the order they were inferred. The types of the partition keys can be deduced by checking the table schema (which will include the partition keys). Not every API will populate this field in the output. For example, Tables.Get will populate it, but Tables.List will not contain this field.

### AvroOptions

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;useAvroLogicalTypes&quot;: boolean
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`useAvroLogicalTypes`

`boolean`

Optional. If sourceFormat is set to "AVRO", indicates whether to interpret logical types as the corresponding BigQuery data type (for example, TIMESTAMP), instead of using the raw type (for example, INTEGER).

### ParquetOptions

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;enumAsString&quot;: boolean,&quot;enableListInference&quot;: boolean,&quot;mapTargetType&quot;: enum (MapTargetType)}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`enumAsString`

`boolean`

Optional. Indicates whether to infer Parquet ENUM logical type as STRING instead of BYTES by default.

`enableListInference`

`boolean`

Optional. Indicates whether to use schema inference specifically for Parquet LIST logical type.

`mapTargetType`

` enum ( MapTargetType  ` )

Optional. Indicates how to represent a Parquet map if present.

### UserDefinedFunctionResource

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;resourceUri&quot;: string,
  &quot;inlineCode&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`resourceUri`

`string`

\[Pick one\] A code resource to load from a Google Cloud Storage URI (gs://bucket/path).

`inlineCode`

`string`

\[Pick one\] An inline resource that contains code for a user-defined function (UDF). Providing a inline code resource is equivalent to providing a URI for a file containing the same code.

### DatasetReference

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;datasetId&quot;: string,
  &quot;projectId&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`datasetId`

`string`

Required. A unique ID for this dataset, without the project name. The ID must contain only letters (a-z, A-Z), numbers (0-9), or underscores (\_). The maximum length is 1,024 characters.

`projectId`

`string`

Optional. The ID of the project containing this dataset.

### QueryParameter

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;parameterType&quot;: {object (QueryParameterType)},&quot;parameterValue&quot;: {object (QueryParameterValue)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`name`

`string`

Optional. If unset, this is a positional parameter. Otherwise, should be unique within a query.

`parameterType`

` object ( QueryParameterType  ` )

Required. The type of this parameter.

`parameterValue`

` object ( QueryParameterValue  ` )

Required. The value of this parameter.

### QueryParameterType

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;type&quot;: string,&quot;arrayType&quot;: {object (QueryParameterType)},&quot;structTypes&quot;: [{object (QueryParameterStructType)}],&quot;rangeElementType&quot;: {object (QueryParameterType)},// Union field _timestamp_precision can be only one of the following:&quot;timestampPrecision&quot;: string// End of list of possible types for union field _timestamp_precision.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`type`

`string`

Required. The top level type of this field.

`arrayType`

` object ( QueryParameterType  ` )

Optional. The type of the array's elements, if this is an array.

`structTypes[]`

` object ( QueryParameterStructType  ` )

Optional. The types of the fields of this struct, in order, if this is a struct.

`rangeElementType`

` object ( QueryParameterType  ` )

Optional. The element type of the range, if this is a range.

Union field `_timestamp_precision` .

`_timestamp_precision` can be only one of the following:

`timestampPrecision`

`string ( int64 format)`

Optional. Precision (maximum number of total digits in base 10) for seconds of TIMESTAMP type.

Possible values include: \* 6 (Default, for TIMESTAMP type with microsecond precision) \* 12 (For TIMESTAMP type with picosecond precision)

### QueryParameterStructType

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;type&quot;: {object (QueryParameterType)},&quot;description&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`name`

`string`

Optional. The name of this field.

`type`

` object ( QueryParameterType  ` )

Required. The type of this field.

`description`

`string`

Optional. Human-oriented description of the field.

### QueryParameterValue

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;value&quot;: string,&quot;arrayValues&quot;: [{object (QueryParameterValue)}],&quot;structValues&quot;: {string: {object (QueryParameterValue)},...},&quot;rangeValue&quot;: {object (RangeValue)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`value`

`string`

Optional. The value of this value, if a simple scalar type.

`arrayValues[]`

` object ( QueryParameterValue  ` )

Optional. The array values, if this is an array type.

`structValues`

` map (key: string, value: object ( QueryParameterValue  ` ))

The struct field values.

An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .

`rangeValue`

` object ( RangeValue  ` )

Optional. The range value, if this is a range type.

### StructValuesEntry

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;key&quot;: string,&quot;value&quot;: {object (QueryParameterValue)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`key`

`string`

`value`

` object ( QueryParameterValue  ` )

### RangeValue

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;start&quot;: {object (QueryParameterValue)},&quot;end&quot;: {object (QueryParameterValue)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`start`

` object ( QueryParameterValue  ` )

Optional. The start value of the range. A missing value represents an unbounded start.

`end`

` object ( QueryParameterValue  ` )

Optional. The end value of the range. A missing value represents an unbounded end.

### SystemVariables

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;types&quot;: {string: {object (StandardSqlDataType)},...},&quot;values&quot;: {object}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`types`

` map (key: string, value: object ( StandardSqlDataType  ` ))

Output only. Data type for each system variable.

An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .

`values`

` object ( Struct  ` format)

Output only. Value for each system variable.

### TypesEntry

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;key&quot;: string,&quot;value&quot;: {object (StandardSqlDataType)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`key`

`string`

`value`

` object ( StandardSqlDataType  ` )

### StandardSqlDataType

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;typeKind&quot;: enum (TypeKind),// Union field sub_type can be only one of the following:&quot;arrayElementType&quot;: {object (StandardSqlDataType)},&quot;structType&quot;: {object (StandardSqlStructType)},&quot;rangeElementType&quot;: {object (StandardSqlDataType)}// End of list of possible types for union field sub_type.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`typeKind`

` enum ( TypeKind  ` )

Required. The top level type of this field. Can be any GoogleSQL data type (e.g., "INT64", "DATE", "ARRAY").

Union field `sub_type` . For complex types, the sub type information. `sub_type` can be only one of the following:

`arrayElementType`

` object ( StandardSqlDataType  ` )

The type of the array's elements, if type\_kind = "ARRAY".

`structType`

` object ( StandardSqlStructType  ` )

The fields of this struct, in order, if type\_kind = "STRUCT".

`rangeElementType`

` object ( StandardSqlDataType  ` )

The type of the range's elements, if type\_kind = "RANGE".

### StandardSqlStructType

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;fields&quot;: [{object (StandardSqlField)}]}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`fields[]`

` object ( StandardSqlField  ` )

Fields within the struct.

### StandardSqlField

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;type&quot;: {object (StandardSqlDataType)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`name`

`string`

Optional. The name of this field. Can be absent for struct fields.

`type`

` object ( StandardSqlDataType  ` )

Optional. The type of this parameter. Absent if not explicitly specified (e.g., CREATE FUNCTION statement can omit the return type; in this case the output parameter does not have this "type" field).

### Struct

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;fields&quot;: {
    string: value,
    ...
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`fields`

` map (key: string, value: value ( Value  ` format))

Unordered map of dynamically typed values.

An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .

### FieldsEntry

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;key&quot;: string,
  &quot;value&quot;: value
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`key`

`string`

`value`

` value ( Value  ` format)

### Value

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field kind can be only one of the following:&quot;nullValue&quot;: null,&quot;numberValue&quot;: number,&quot;stringValue&quot;: string,&quot;boolValue&quot;: boolean,&quot;structValue&quot;: {object},&quot;listValue&quot;: array// End of list of possible types for union field kind.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `kind` . The kind of value. `kind` can be only one of the following:

`nullValue`

`null`

Represents a JSON `null` .

`numberValue`

`number`

Represents a JSON number. Must not be `NaN` , `Infinity` or `-Infinity` , since those are not supported in JSON. This also cannot represent large Int64 values, since JSON format generally does not support them in its number type.

`stringValue`

`string`

Represents a JSON string.

`boolValue`

`boolean`

Represents a JSON boolean ( `true` or `false` literal in JSON).

`structValue`

` object ( Struct  ` format)

Represents a JSON object.

`listValue`

` array ( ListValue  ` format)

Represents a JSON array.

### ListValue

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;values&quot;: [
    value
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`values[]`

` value ( Value  ` format)

Repeated field of dynamically typed values.

### TimePartitioning

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;type&quot;: string,
  &quot;expirationMs&quot;: string,
  &quot;field&quot;: string,
  &quot;requirePartitionFilter&quot;: boolean
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`type`

`string`

Required. The supported types are DAY, HOUR, MONTH, and YEAR, which will generate one partition per day, hour, month, and year, respectively.

`expirationMs`

`string ( Int64Value format)`

Optional. Number of milliseconds for which to keep the storage for a partition. A wrapper is used here because 0 is an invalid value.

`field`

`string`

Optional. If not set, the table is partitioned by pseudo column '\_PARTITIONTIME'; if set, the table is partitioned by this field. The field must be a top-level TIMESTAMP or DATE field. Its mode must be NULLABLE or REQUIRED. A wrapper is used here because an empty string is an invalid value.

` requirePartitionFilter (deprecated)  `

`boolean`

> This item is deprecated\!

If set to true, queries over this table require a partition filter that can be used for partition elimination to be specified. This field is deprecated; please set the field with the same name on the table itself instead. This field needs a wrapper because we want to output the default value, false, if the user explicitly set it.

### RangePartitioning

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;field&quot;: string,&quot;range&quot;: {object (Range)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`field`

`string`

Required. The name of the column to partition the table on. It must be a top-level, INT64 column whose mode is NULLABLE or REQUIRED.

`range`

` object ( Range  ` )

Defines the ranges for range partitioning.

### Range

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;start&quot;: string,
  &quot;end&quot;: string,
  &quot;interval&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`start`

`string`

Required. The start of range partitioning, inclusive. This field is an INT64 value represented as a string.

`end`

`string`

Required. The end of range partitioning, exclusive. This field is an INT64 value represented as a string.

`interval`

`string`

Required. The width of each interval. This field is an INT64 value represented as a string.

### Clustering

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;fields&quot;: [
    string
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`fields[]`

`string`

One or more fields on which data should be clustered. Only top-level, non-repeated, simple-type fields are supported. The ordering of the clustering fields should be prioritized from most to least important for filtering purposes.

For additional information, see [Introduction to clustered tables](https://cloud.google.com/bigquery/docs/clustered-tables#limitations) .

### EncryptionConfiguration

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;kmsKeyName&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`kmsKeyName`

`string`

Optional. Describes the Cloud KMS encryption key that will be used to protect destination BigQuery table. The BigQuery Service Account associated with your project requires access to this encryption key.

### ScriptOptions

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;statementTimeoutMs&quot;: string,&quot;statementByteBudget&quot;: string,&quot;keyResultStatement&quot;: enum (KeyResultStatementKind)}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`statementTimeoutMs`

`string ( Int64Value format)`

Timeout period for each statement in a script.

`statementByteBudget`

`string ( Int64Value format)`

Limit on the number of bytes billed per statement. Exceeding this budget results in an error.

`keyResultStatement`

` enum ( KeyResultStatementKind  ` )

Determines which statement in the script represents the "key result", used to populate the schema and query results of the script job. Default is LAST.

### ConnectionProperty

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;key&quot;: string,
  &quot;value&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`key`

`string`

The key of the property to set.

`value`

`string`

The value of the property to set.

### SecureContext

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;secureParameterEntries&quot;: {
    object
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`secureParameterEntries`

` object ( Struct  ` format)

Optional. A set of key-value pairs representing the secure parameter values. They can be retrieved via the SECURE\_CONTEXT() function and used to modify the run-time behavior of a query.

### JobConfigurationLoad

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;sourceUris&quot;: [string],&quot;fileSetSpecType&quot;: enum (FileSetSpecType),&quot;schema&quot;: {object (TableSchema)},&quot;destinationTable&quot;: {object (TableReference)},&quot;destinationTableProperties&quot;: {object (DestinationTableProperties)},&quot;createDisposition&quot;: string,&quot;writeDisposition&quot;: string,&quot;nullMarker&quot;: string,&quot;fieldDelimiter&quot;: string,&quot;skipLeadingRows&quot;: integer,&quot;encoding&quot;: string,&quot;quote&quot;: string,&quot;maxBadRecords&quot;: integer,&quot;schemaInlineFormat&quot;: string,&quot;schemaInline&quot;: string,&quot;allowQuotedNewlines&quot;: boolean,&quot;sourceFormat&quot;: string,&quot;allowJaggedRows&quot;: boolean,&quot;ignoreUnknownValues&quot;: boolean,&quot;projectionFields&quot;: [string],&quot;autodetect&quot;: boolean,&quot;schemaUpdateOptions&quot;: [string],&quot;timePartitioning&quot;: {object (TimePartitioning)},&quot;rangePartitioning&quot;: {object (RangePartitioning)},&quot;clustering&quot;: {object (Clustering)},&quot;destinationEncryptionConfiguration&quot;: {object (EncryptionConfiguration)},&quot;useAvroLogicalTypes&quot;: boolean,&quot;referenceFileSchemaUri&quot;: string,&quot;hivePartitioningOptions&quot;: {object (HivePartitioningOptions)},&quot;decimalTargetTypes&quot;: [enum (DecimalTargetType)],&quot;thriftOptions&quot;: {object (ThriftOptions)},&quot;jsonExtension&quot;: enum (JsonExtension),&quot;parquetOptions&quot;: {object (ParquetOptions)},&quot;preserveAsciiControlCharacters&quot;: boolean,&quot;connectionProperties&quot;: [{object (ConnectionProperty)}],&quot;createSession&quot;: boolean,&quot;columnNameCharacterMap&quot;: enum (ColumnNameCharacterMap),&quot;copyFilesOnly&quot;: boolean,&quot;timeZone&quot;: string,&quot;nullMarkers&quot;: [string],&quot;sourceColumnMatch&quot;: enum (SourceColumnMatch),&quot;timestampTargetPrecision&quot;: [integer],// Union field _date_format can be only one of the following:&quot;dateFormat&quot;: string// End of list of possible types for union field _date_format.// Union field _datetime_format can be only one of the following:&quot;datetimeFormat&quot;: string// End of list of possible types for union field _datetime_format.// Union field _time_format can be only one of the following:&quot;timeFormat&quot;: string// End of list of possible types for union field _time_format.// Union field _timestamp_format can be only one of the following:&quot;timestampFormat&quot;: string// End of list of possible types for union field _timestamp_format.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`sourceUris[]`

`string`

\[Required\] The fully-qualified URIs that point to your data in Google Cloud. For Google Cloud Storage URIs: Each URI can contain one '\*' wildcard character and it must come after the 'bucket' name. Size limits related to load jobs apply to external data sources. For Google Cloud Bigtable URIs: Exactly one URI can be specified and it has be a fully specified and valid HTTPS URL for a Google Cloud Bigtable table. For Google Cloud Datastore backups: Exactly one URI can be specified. Also, the '\*' wildcard character is not allowed.

`fileSetSpecType`

` enum ( FileSetSpecType  ` )

Optional. Specifies how source URIs are interpreted for constructing the file set to load. By default, source URIs are expanded against the underlying storage. You can also specify manifest files to control how the file set is constructed. This option is only applicable to object storage systems.

`schema`

` object ( TableSchema  ` )

Optional. The schema for the destination table. The schema can be omitted if the destination table already exists, or if you're loading data from Google Cloud Datastore.

`destinationTable`

` object ( TableReference  ` )

\[Required\] The destination table to load the data into.

`destinationTableProperties`

` object ( DestinationTableProperties  ` )

Optional. \[Experimental\] Properties with which to create the destination table if it is new.

`createDisposition`

`string`

Optional. Specifies whether the job is allowed to create new tables. The following values are supported:

  - CREATE\_IF\_NEEDED: If the table does not exist, BigQuery creates the table.
  - CREATE\_NEVER: The table must already exist. If it does not, a 'notFound' error is returned in the job result. The default value is CREATE\_IF\_NEEDED. Creation, truncation and append actions occur as one atomic update upon job completion.

`writeDisposition`

`string`

Optional. Specifies the action that occurs if the destination table already exists. The following values are supported:

  - WRITE\_TRUNCATE: If the table already exists, BigQuery overwrites the data, removes the constraints and uses the schema from the load job.
  - WRITE\_TRUNCATE\_DATA: If the table already exists, BigQuery overwrites the data, but keeps the constraints and schema of the existing table.
  - WRITE\_APPEND: If the table already exists, BigQuery appends the data to the table.
  - WRITE\_EMPTY: If the table already exists and contains data, a 'duplicate' error is returned in the job result.

The default value is WRITE\_APPEND. Each action is atomic and only occurs if BigQuery is able to complete the job successfully. Creation, truncation and append actions occur as one atomic update upon job completion.

`nullMarker`

`string`

Optional. Specifies a string that represents a null value in a CSV file. For example, if you specify "\\N", BigQuery interprets "\\N" as a null value when loading a CSV file. The default value is the empty string. If you set this property to a custom value, BigQuery throws an error if an empty string is present for all data types except for STRING and BYTE. For STRING and BYTE columns, BigQuery interprets the empty string as an empty value.

`fieldDelimiter`

`string`

Optional. The separator character for fields in a CSV file. The separator is interpreted as a single byte. For files encoded in ISO-8859-1, any single character can be used as a separator. For files encoded in UTF-8, characters represented in decimal range 1-127 (U+0001-U+007F) can be used without any modification. UTF-8 characters encoded with multiple bytes (i.e. U+0080 and above) will have only the first byte used for separating fields. The remaining bytes will be treated as a part of the field. BigQuery also supports the escape sequence "\\t" (U+0009) to specify a tab separator. The default value is comma (",", U+002C).

`skipLeadingRows`

`integer`

Optional. The number of rows at the top of a CSV file that BigQuery will skip when loading the data. The default value is 0. This property is useful if you have header rows in the file that should be skipped. When autodetect is on, the behavior is the following:

  - skipLeadingRows unspecified - Autodetect tries to detect headers in the first row. If they are not detected, the row is read as data. Otherwise data is read starting from the second row.
  - skipLeadingRows is 0 - Instructs autodetect that there are no headers and data should be read starting from the first row.
  - skipLeadingRows = N \> 0 - Autodetect skips N-1 rows and tries to detect headers in row N. If headers are not detected, row N is just skipped. Otherwise row N is used to extract column names for the detected schema.

`encoding`

`string`

Optional. The character encoding of the data. The supported values are UTF-8, ISO-8859-1, UTF-16BE, UTF-16LE, UTF-32BE, and UTF-32LE. The default value is UTF-8. BigQuery decodes the data after the raw, binary data has been split using the values of the `quote` and `fieldDelimiter` properties.

If you don't specify an encoding, or if you specify a UTF-8 encoding when the CSV file is not UTF-8 encoded, BigQuery attempts to convert the data to UTF-8. Generally, your data loads successfully, but it may not match byte-for-byte what you expect. To avoid this, specify the correct encoding by using the `--encoding` flag.

If BigQuery can't convert a character other than the ASCII `0` character, BigQuery converts the character to the standard Unicode replacement character: �.

`quote`

`string`

Optional. The value that is used to quote data sections in a CSV file. BigQuery converts the string to ISO-8859-1 encoding, and then uses the first byte of the encoded string to split the data in its raw, binary state. The default value is a double-quote ('"'). If your data does not contain quoted sections, set the property value to an empty string. If your data contains quoted newline characters, you must also set the allowQuotedNewlines property to true. To include the specific quote character within a quoted value, precede it with an additional matching quote character. For example, if you want to escape the default character ' " ', use ' "" '. @default "

`maxBadRecords`

`integer`

Optional. The maximum number of bad records that BigQuery can ignore when running the job. If the number of bad records exceeds this value, an invalid error is returned in the job result. The default value is 0, which requires that all records are valid. This is only supported for CSV and NEWLINE\_DELIMITED\_JSON file formats.

`schemaInlineFormat`

`string`

\[Deprecated\] The format of the schemaInline property.

`schemaInline`

`string`

\[Deprecated\] The inline schema. For CSV schemas, specify as "Field1:Type1\[,Field2:Type2\]\*". For example, "foo:STRING, bar:INTEGER, baz:FLOAT".

`allowQuotedNewlines`

`boolean`

Indicates if BigQuery should allow quoted data sections that contain newline characters in a CSV file. The default value is false.

`sourceFormat`

`string`

Optional. The format of the data files. For CSV files, specify "CSV". For datastore backups, specify "DATASTORE\_BACKUP". For newline-delimited JSON, specify "NEWLINE\_DELIMITED\_JSON". For Avro, specify "AVRO". For parquet, specify "PARQUET". For orc, specify "ORC". The default value is CSV.

`allowJaggedRows`

`boolean`

Optional. Accept rows that are missing trailing optional columns. The missing values are treated as nulls. If false, records with missing trailing columns are treated as bad records, and if there are too many bad records, an invalid error is returned in the job result. The default value is false. Only applicable to CSV, ignored for other formats.

`ignoreUnknownValues`

`boolean`

Optional. Indicates if BigQuery should allow extra values that are not represented in the table schema. If true, the extra values are ignored. If false, records with extra columns are treated as bad records, and if there are too many bad records, an invalid error is returned in the job result. The default value is false. The sourceFormat property determines what BigQuery treats as an extra value: CSV: Trailing columns JSON: Named values that don't match any column names in the table schema Avro, Parquet, ORC: Fields in the file schema that don't exist in the table schema.

`projectionFields[]`

`string`

If sourceFormat is set to "DATASTORE\_BACKUP", indicates which entity properties to load into BigQuery from a Cloud Datastore backup. Property names are case sensitive and must be top-level properties. If no properties are specified, BigQuery loads all properties. If any named property isn't found in the Cloud Datastore backup, an invalid error is returned in the job result.

`autodetect`

`boolean`

Optional. Indicates if we should automatically infer the options and schema for CSV and JSON sources.

`schemaUpdateOptions[]`

`string`

Allows the schema of the destination table to be updated as a side effect of the load job if a schema is autodetected or supplied in the job configuration. Schema update options are supported in three cases: when writeDisposition is WRITE\_APPEND; when writeDisposition is WRITE\_TRUNCATE\_DATA; when writeDisposition is WRITE\_TRUNCATE and the destination table is a partition of a table, specified by partition decorators. For normal tables, WRITE\_TRUNCATE will always overwrite the schema. One or more of the following values are specified:

  - ALLOW\_FIELD\_ADDITION: allow adding a nullable field to the schema.
  - ALLOW\_FIELD\_RELAXATION: allow relaxing a required field in the original schema to nullable.

`timePartitioning`

` object ( TimePartitioning  ` )

Time-based partitioning specification for the destination table. Only one of timePartitioning and rangePartitioning should be specified.

`rangePartitioning`

` object ( RangePartitioning  ` )

Range partitioning specification for the destination table. Only one of timePartitioning and rangePartitioning should be specified.

`clustering`

` object ( Clustering  ` )

Clustering specification for the destination table.

`destinationEncryptionConfiguration`

` object ( EncryptionConfiguration  ` )

Custom encryption configuration (e.g., Cloud KMS keys)

`useAvroLogicalTypes`

`boolean`

Optional. If sourceFormat is set to "AVRO", indicates whether to interpret logical types as the corresponding BigQuery data type (for example, TIMESTAMP), instead of using the raw type (for example, INTEGER).

`referenceFileSchemaUri`

`string`

Optional. The user can provide a reference file with the reader schema. This file is only loaded if it is part of source URIs, but is not loaded otherwise. It is enabled for the following formats: AVRO, PARQUET, ORC.

`hivePartitioningOptions`

` object ( HivePartitioningOptions  ` )

Optional. When set, configures hive partitioning support. Not all storage formats support hive partitioning -- requesting hive partitioning on an unsupported format will lead to an error, as will providing an invalid specification.

`decimalTargetTypes[]`

` enum ( DecimalTargetType  ` )

Defines the list of possible SQL data types to which the source decimal values are converted. This list and the precision and the scale parameters of the decimal field determine the target type. In the order of NUMERIC, BIGNUMERIC, and STRING, a type is picked if it is in the specified list and if it supports the precision and the scale. STRING supports all precision and scale values. If none of the listed types supports the precision and the scale, the type supporting the widest range in the specified list is picked, and if a value exceeds the supported range when reading the data, an error will be thrown.

Example: Suppose the value of this field is \["NUMERIC", "BIGNUMERIC"\]. If (precision,scale) is:

  - (38,9) -\> NUMERIC;
  - (39,9) -\> BIGNUMERIC (NUMERIC cannot hold 30 integer digits);
  - (38,10) -\> BIGNUMERIC (NUMERIC cannot hold 10 fractional digits);
  - (76,38) -\> BIGNUMERIC;
  - (77,38) -\> BIGNUMERIC (error if value exceeds supported range).

This field cannot contain duplicate types. The order of the types in this field is ignored. For example, \["BIGNUMERIC", "NUMERIC"\] is the same as \["NUMERIC", "BIGNUMERIC"\] and NUMERIC always takes precedence over BIGNUMERIC.

Defaults to \["NUMERIC", "STRING"\] for ORC and \["NUMERIC"\] for the other file formats.

`thriftOptions`

` object ( ThriftOptions  ` )

Optional. \[Experimental\] The load options for Apache Thrift serialized data. It defines the source of IDL bundle that should be used to be parsed as the schema and deserialization options to parse Thrift data.

`jsonExtension`

` enum ( JsonExtension  ` )

Optional. Load option to be used together with source\_format newline-delimited JSON to indicate that a variant of JSON is being loaded. To load newline-delimited GeoJSON, specify GEOJSON (and source\_format must be set to NEWLINE\_DELIMITED\_JSON).

`parquetOptions`

` object ( ParquetOptions  ` )

Optional. Additional properties to set if sourceFormat is set to PARQUET.

`preserveAsciiControlCharacters`

`boolean`

Optional. When sourceFormat is set to "CSV", this indicates whether the embedded ASCII control characters (the first 32 characters in the ASCII-table, from '\\x00' to '\\x1F') are preserved.

`connectionProperties[]`

` object ( ConnectionProperty  ` )

Optional. Connection properties which can modify the load job behavior. Currently, only the 'session\_id' connection property is supported, and is used to resolve \_SESSION appearing as the dataset id.

`createSession`

`boolean`

Optional. If this property is true, the job creates a new session using a randomly generated session\_id. To continue using a created session with subsequent queries, pass the existing session identifier as a `ConnectionProperty` value. The session identifier is returned as part of the `SessionInfo` message within the query statistics.

The new session's location will be set to `Job.JobReference.location` if it is present, otherwise it's set to the default location based on existing routing logic.

`columnNameCharacterMap`

` enum ( ColumnNameCharacterMap  ` )

Optional. Character map supported for column names in CSV/Parquet loads. Defaults to STRICT and can be overridden by Project Config Service. Using this option with unsupporting load formats will result in an error.

`copyFilesOnly`

`boolean`

Optional. \[Experimental\] Configures the load job to copy files directly to the destination BigLake managed table, bypassing file content reading and rewriting.

Copying files only is supported when all the following are true:

  - `source_uris` are located in the same Cloud Storage location as the destination table's `storage_uri` location.
  - `source_format` is `PARQUET` .
  - `destination_table` is an existing BigLake managed table. The table's schema does not have flexible column names. The table's columns do not have type parameters other than precision and scale.
  - No options other than the above are specified.

`timeZone`

`string`

Optional. Default time zone that will apply when parsing timestamp values that have no specific time zone.

`nullMarkers[]`

`string`

Optional. A list of strings represented as SQL NULL value in a CSV file.

null\_marker and null\_markers can't be set at the same time. If null\_marker is set, null\_markers has to be not set. If null\_markers is set, null\_marker has to be not set. If both null\_marker and null\_markers are set at the same time, a user error would be thrown. Any strings listed in null\_markers, including empty string would be interpreted as SQL NULL. This applies to all column types.

`sourceColumnMatch`

` enum ( SourceColumnMatch  ` )

Optional. Controls the strategy used to match loaded columns to the schema. If not set, a sensible default is chosen based on how the schema is provided. If autodetect is used, then columns are matched by name. Otherwise, columns are matched by position. This is done to keep the behavior backward-compatible.

`timestampTargetPrecision[]`

`integer`

Precisions (maximum number of total digits in base 10) for seconds of TIMESTAMP types that are allowed to the destination table for autodetection mode.

Available for the formats: CSV, PARQUET, AVRO, and Iceberg External Table.

Possible values include: Not Specified, \[\], or \[6\]: timestamp(6) for all auto detected TIMESTAMP columns \[6, 12\]: timestamp(6) for all auto detected TIMESTAMP columns that have less than 6 digits of subseconds. timestamp(12) for all auto detected TIMESTAMP columns that have more than 6 digits of subseconds. \[12\]: timestamp(12) for all auto detected TIMESTAMP columns.

The order of the elements in this array is ignored. Inputs that have higher precision than the highest target precision in this array will be truncated.

Union field `_date_format` .

`_date_format` can be only one of the following:

`dateFormat`

`string`

Optional. Date format used for parsing DATE values.

Union field `_datetime_format` .

`_datetime_format` can be only one of the following:

`datetimeFormat`

`string`

Optional. Date format used for parsing DATETIME values.

Union field `_time_format` .

`_time_format` can be only one of the following:

`timeFormat`

`string`

Optional. Date format used for parsing TIME values.

Union field `_timestamp_format` .

`_timestamp_format` can be only one of the following:

`timestampFormat`

`string`

Optional. Date format used for parsing TIMESTAMP values.

### DestinationTableProperties

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
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

`friendlyName`

`string`

Optional. Friendly name for the destination table. If the table already exists, it should be same as the existing friendly name.

`description`

`string`

Optional. The description for the destination table. This will only be used if the destination table is newly created. If the table already exists and a value different than the current description is provided, the job will fail.

`labels`

`map (key: string, value: string)`

Optional. The labels associated with this table. You can use these to organize and group your tables. This will only be used if the destination table is newly created. If the table already exists and labels are different than the current labels are provided, the job will fail.

An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .

### LabelsEntry

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;key&quot;: string,
  &quot;value&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`key`

`string`

`value`

`string`

### ThriftOptions

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;schemaIdlRootDir&quot;: string,&quot;schemaIdlUri&quot;: string,&quot;schemaStruct&quot;: string,&quot;deserializationOption&quot;: enum (DeserializationOption),&quot;framingOption&quot;: enum (FramingOption),&quot;boundaryBytes&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`schemaIdlRootDir`

`string`

Required. The root directory of the IDL file bundle defining the schema. All IDL files that are used to parse the schema should be in this directory. This directory should be different from the source\_uris.

`schemaIdlUri`

`string`

Required. The Thrift IDL file in the `schema_idl_root_dir` that should be used as the root file to parse the schema. All included idl files in the `schema_idl_uri` should also be in the `schema_idl_root_dir` or its sub-directory.

`schemaStruct`

`string`

Required. The root struct specified in `schema_idl_uri` that should be used to parse the schema.

`deserializationOption`

` enum ( DeserializationOption  ` )

Optional. `deserialization_option` sets how the serialized Thrift should be deserialized. The following options are supported:

  - THRIFT\_BINARY\_PROTOCOL\_OPTION: using TBinaryProtocol to deserialize the data.

`framingOption`

` enum ( FramingOption  ` )

Optional. Framing in Thrift means 4 bytes slipped in front of the serialized record or data block to inidicate the size of the followed record or data block. The following options are support:

  - NOT\_FRAMED: Serialized Thrift records or data blocks are not framed, there are no 4-byte record size in front of the record.

  - FRAMED\_WITH\_BIG\_ENDIAN: Serialized Thrift records or data blocks are framed with the 4-byte record size in big endian.

  - FRAMED\_WITH\_LITTLE\_ENDIAN: Serialized Thrift records or data blocks are framed with the 4-byte record size in little endian.

One option to frame Thrift record at serialization time is using `TFramedTransport` , which writes the 4-byte record or data block size in big endian. By default `framing_option` is set to "NOT\_FRAMED".

`boundaryBytes`

`string ( bytes format)`

Optional. Sequence of bytes used to separate two serialized Thrift data blocks. When it's used with `framing_option` , the `boundary_bytes` are expected to be in front of the framed block.

A base64-encoded string.

### JobConfigurationTableCopy

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;sourceTable&quot;: {object (TableReference)},&quot;sourceTables&quot;: [{object (TableReference)}],&quot;destinationTable&quot;: {object (TableReference)},&quot;createDisposition&quot;: string,&quot;writeDisposition&quot;: string,&quot;destinationEncryptionConfiguration&quot;: {object (EncryptionConfiguration)},&quot;operationType&quot;: enum (OperationType),&quot;destinationExpirationTime&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`sourceTable`

` object ( TableReference  ` )

\[Pick one\] Source table to copy.

`sourceTables[]`

` object ( TableReference  ` )

\[Pick one\] Source tables to copy.

`destinationTable`

` object ( TableReference  ` )

\[Required\] The destination table.

`createDisposition`

`string`

Optional. Specifies whether the job is allowed to create new tables. The following values are supported:

  - CREATE\_IF\_NEEDED: If the table does not exist, BigQuery creates the table.
  - CREATE\_NEVER: The table must already exist. If it does not, a 'notFound' error is returned in the job result.

The default value is CREATE\_IF\_NEEDED. Creation, truncation and append actions occur as one atomic update upon job completion.

`writeDisposition`

`string`

Optional. Specifies the action that occurs if the destination table already exists. The following values are supported:

  - WRITE\_TRUNCATE: If the table already exists, BigQuery overwrites the table data and uses the schema and table constraints from the source table.
  - WRITE\_APPEND: If the table already exists, BigQuery appends the data to the table.
  - WRITE\_EMPTY: If the table already exists and contains data, a 'duplicate' error is returned in the job result.

The default value is WRITE\_EMPTY. Each action is atomic and only occurs if BigQuery is able to complete the job successfully. Creation, truncation and append actions occur as one atomic update upon job completion.

`destinationEncryptionConfiguration`

` object ( EncryptionConfiguration  ` )

Custom encryption configuration (e.g., Cloud KMS keys).

`operationType`

` enum ( OperationType  ` )

Optional. Supported operation types in table copy job.

`destinationExpirationTime`

` string ( Timestamp  ` format)

Optional. The time when the destination table expires. Expired tables will be deleted and their storage reclaimed.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

### Timestamp

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;seconds&quot;: string,
  &quot;nanos&quot;: integer
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`seconds`

`string ( int64 format)`

Represents seconds of UTC time since Unix epoch 1970-01-01T00:00:00Z. Must be between -62135596800 and 253402300799 inclusive (which corresponds to 0001-01-01T00:00:00Z to 9999-12-31T23:59:59Z).

`nanos`

`integer`

Non-negative fractions of a second at nanosecond resolution. This field is the nanosecond portion of the duration, not an alternative to seconds. Negative second values with fractions must still have non-negative nanos values that count forward in time. Must be between 0 and 999,999,999 inclusive.

### JobConfigurationExtract

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;destinationUri&quot;: string,&quot;destinationUris&quot;: [string],&quot;printHeader&quot;: boolean,&quot;fieldDelimiter&quot;: string,&quot;destinationFormat&quot;: string,&quot;compression&quot;: string,&quot;useAvroLogicalTypes&quot;: boolean,&quot;modelExtractOptions&quot;: {object (ModelExtractOptions)},&quot;nativeGeographyExportEnabled&quot;: boolean,// Union field source can be only one of the following:&quot;sourceTable&quot;: {object (TableReference)},&quot;sourceModel&quot;: {object (ModelReference)}// End of list of possible types for union field source.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`destinationUri`

`string`

\[Pick one\] DEPRECATED: Use destinationUris instead, passing only one URI as necessary. The fully-qualified Google Cloud Storage URI where the extracted table should be written.

`destinationUris[]`

`string`

\[Pick one\] A list of fully-qualified Google Cloud Storage URIs where the extracted table should be written.

`printHeader`

`boolean`

Optional. Whether to print out a header row in the results. Default is true. Not applicable when extracting models.

`fieldDelimiter`

`string`

Optional. When extracting data in CSV format, this defines the delimiter to use between fields in the exported data. Default is ','. Not applicable when extracting models.

`destinationFormat`

`string`

Optional. The exported file format. Possible values include CSV, NEWLINE\_DELIMITED\_JSON, PARQUET, or AVRO for tables and ML\_TF\_SAVED\_MODEL or ML\_XGBOOST\_BOOSTER for models. The default value for tables is CSV. Tables with nested or repeated fields cannot be exported as CSV. The default value for models is ML\_TF\_SAVED\_MODEL.

`compression`

`string`

Optional. The compression type to use for exported files. Possible values include DEFLATE, GZIP, NONE, SNAPPY, and ZSTD. The default value is NONE. Not all compression formats are support for all file formats. DEFLATE is only supported for Avro. ZSTD is only supported for Parquet. Not applicable when extracting models.

`useAvroLogicalTypes`

`boolean`

Whether to use logical types when extracting to AVRO format. Not applicable when extracting models.

`modelExtractOptions`

` object ( ModelExtractOptions  ` )

Optional. Model extract options only applicable when extracting models.

`nativeGeographyExportEnabled`

`boolean`

Optional. Applicable to formats: PARQUET. If enabled, BigQuery to Parquet export will write the native Parquet Geography type instead of the default GeoParquet type.

Union field `source` . Required. Source reference for the export. `source` can be only one of the following:

`sourceTable`

` object ( TableReference  ` )

A reference to the table being exported.

`sourceModel`

` object ( ModelReference  ` )

A reference to the model being exported.

### ModelReference

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;projectId&quot;: string,
  &quot;datasetId&quot;: string,
  &quot;modelId&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`projectId`

`string`

Required. The ID of the project containing this model.

`datasetId`

`string`

Required. The ID of the dataset containing this model.

`modelId`

`string`

Required. The ID of the model. The ID must contain only letters (a-z, A-Z), numbers (0-9), or underscores (\_). The maximum length is 1,024 characters.

### ModelExtractOptions

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;trialId&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`trialId`

`string ( Int64Value format)`

The 1-based ID of the trial to be exported from a hyperparameter tuning model. If not specified, the trial with id = [Model](https://cloud.google.com/bigquery/docs/reference/rest/v2/models#resource:-model) .defaultTrialId is exported. This field is ignored for models not trained with hyperparameter tuning.

### LabelsEntry

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;key&quot;: string,
  &quot;value&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`key`

`string`

`value`

`string`

### JobReference

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;projectId&quot;: string,
  &quot;jobId&quot;: string,
  &quot;location&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`projectId`

`string`

Required. The ID of the project containing this job.

`jobId`

`string`

Required. The ID of the job. The ID must contain only letters (a-z, A-Z), numbers (0-9), underscores (\_), or dashes (-). The maximum length is 1,024 characters.

`location`

`string`

Optional. The geographic location of the job. The default value is US.

For more information about BigQuery locations, see: <https://cloud.google.com/bigquery/docs/locations>

### JobStatistics

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;creationTime&quot;: string,&quot;startTime&quot;: string,&quot;endTime&quot;: string,&quot;totalBytesProcessed&quot;: string,&quot;completionRatio&quot;: number,&quot;quotaDeferments&quot;: [string],&quot;query&quot;: {object (JobStatistics2)},&quot;load&quot;: {object (JobStatistics3)},&quot;extract&quot;: {object (JobStatistics4)},&quot;copy&quot;: {object (CopyJobStatistics)},&quot;totalSlotMs&quot;: string,&quot;reservationUsage&quot;: [{object (ReservationResourceUsage)}],&quot;reservation_id&quot;: string,&quot;numChildJobs&quot;: string,&quot;parentJobId&quot;: string,&quot;scriptStatistics&quot;: {object (ScriptStatistics)},&quot;rowLevelSecurityStatistics&quot;: {object (RowLevelSecurityStatistics)},&quot;dataMaskingStatistics&quot;: {object (DataMaskingStatistics)},&quot;transactionInfo&quot;: {object (TransactionInfo)},&quot;sessionInfo&quot;: {object (SessionInfo)},&quot;finalExecutionDurationMs&quot;: string,&quot;edition&quot;: enum (ReservationEdition),&quot;reservationGroupPath&quot;: [string],&quot;globalQueryRemoteRegions&quot;: [string],&quot;parentGlobalQueryJob&quot;: {object (JobReference)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`creationTime`

`string ( int64 format)`

Output only. Creation time of this job, in milliseconds since the epoch. This field will be present on all jobs.

`startTime`

`string ( int64 format)`

Output only. Start time of this job, in milliseconds since the epoch. This field will be present when the job transitions from the PENDING state to either RUNNING or DONE.

`endTime`

`string ( int64 format)`

Output only. End time of this job, in milliseconds since the epoch. This field will be present whenever a job is in the DONE state.

`totalBytesProcessed`

`string ( Int64Value format)`

Output only. Total bytes processed for the job.

`completionRatio`

`number`

Output only. \[TrustedTester\] Job progress (0.0 -\> 1.0) for LOAD and EXTRACT jobs.

`quotaDeferments[]`

`string`

Output only. Quotas which delayed this job's start time.

`query`

` object ( JobStatistics2  ` )

Output only. Statistics for a query job.

`load`

` object ( JobStatistics3  ` )

Output only. Statistics for a load job.

`extract`

` object ( JobStatistics4  ` )

Output only. Statistics for an extract job.

`copy`

` object ( CopyJobStatistics  ` )

Output only. Statistics for a copy job.

`totalSlotMs`

`string ( Int64Value format)`

Output only. Slot-milliseconds for the job.

` reservationUsage[] (deprecated)  `

` object ( ReservationResourceUsage  ` )

> This item is deprecated\!

Output only. Job resource usage breakdown by reservation. This field reported misleading information and will no longer be populated.

`reservation_id`

`string`

Output only. Name of the primary reservation assigned to this job. Note that this could be different than reservations reported in the reservation usage field if parent reservations were used to execute this job.

`numChildJobs`

`string ( int64 format)`

Output only. Number of child jobs executed.

`parentJobId`

`string`

Output only. If this is a child job, specifies the job ID of the parent.

`scriptStatistics`

` object ( ScriptStatistics  ` )

Output only. If this a child job of a script, specifies information about the context of this job within the script.

`rowLevelSecurityStatistics`

` object ( RowLevelSecurityStatistics  ` )

Output only. Statistics for row-level security. Present only for query and extract jobs.

`dataMaskingStatistics`

` object ( DataMaskingStatistics  ` )

Output only. Statistics for data-masking. Present only for query and extract jobs.

`transactionInfo`

` object ( TransactionInfo  ` )

Output only. \[Alpha\] Information of the multi-statement transaction if this job is part of one.

This property is only expected on a child job or a job that is in a session. A script parent job is not part of the transaction started in the script.

`sessionInfo`

` object ( SessionInfo  ` )

Output only. Information of the session if this job is part of one.

`finalExecutionDurationMs`

`string ( int64 format)`

Output only. The duration in milliseconds of the execution of the final attempt of this job, as BigQuery may internally re-attempt to execute the job.

`edition`

` enum ( ReservationEdition  ` )

Output only. Name of edition corresponding to the reservation for this job at the time of this update.

`reservationGroupPath[]`

`string`

Output only. The reservation group path of the reservation assigned to this job. This field has a limit of 10 nested reservation groups. This is to maintain consistency between reservations info schema and jobs info schema. The first reservation group is the root reservation group and the last is the leaf or lowest level reservation group.

`globalQueryRemoteRegions[]`

`string`

Output only. The list of remote regions from which a global query accesses data.

This field is populated only for parent global query jobs in the primary execution region. It is empty for child global query jobs and single-region queries. For more information, see [Global queries](https://cloud.google.com/bigquery/docs/global-queries) .

`parentGlobalQueryJob`

` object ( JobReference  ` )

Output only. Reference to the parent global query job, if this is a child global query job.

This field is populated only for child global query jobs (remote subqueries or cross-region table copy jobs) executed in remote regions on behalf of a global query. It contains the project ID, job ID, and location of the parent global query job. It is unset for parent global query jobs and single-region queries. For more information, see [Global queries](https://cloud.google.com/bigquery/docs/global-queries) .

### DoubleValue

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;value&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`value`

`number`

The double value.

### JobStatistics2

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;queryPlan&quot;: [{object (ExplainQueryStage)}],&quot;estimatedBytesProcessed&quot;: string,&quot;timeline&quot;: [{object (QueryTimelineSample)}],&quot;totalPartitionsProcessed&quot;: string,&quot;totalBytesProcessed&quot;: string,&quot;totalBytesProcessedAccuracy&quot;: string,&quot;totalBytesBilled&quot;: string,&quot;billingTier&quot;: integer,&quot;totalSlotMs&quot;: string,&quot;reservationUsage&quot;: [{object (ReservationResourceUsage)}],&quot;cacheHit&quot;: boolean,&quot;referencedTables&quot;: [{object (TableReference)}],&quot;referencedRoutines&quot;: [{object (RoutineReference)}],&quot;referencedPropertyGraphs&quot;: [{object (PropertyGraphReference)}],&quot;schema&quot;: {object (TableSchema)},&quot;numDmlAffectedRows&quot;: string,&quot;dmlStats&quot;: {object (DmlStats)},&quot;undeclaredQueryParameters&quot;: [{object (QueryParameter)}],&quot;statementType&quot;: string,&quot;ddlOperationPerformed&quot;: string,&quot;ddlTargetTable&quot;: {object (TableReference)},&quot;ddlDestinationTable&quot;: {object (TableReference)},&quot;ddlTargetRowAccessPolicy&quot;: {object (RowAccessPolicyReference)},&quot;ddlAffectedRowAccessPolicyCount&quot;: string,&quot;ddlTargetRoutine&quot;: {object (RoutineReference)},&quot;ddlTargetDataset&quot;: {object (DatasetReference)},&quot;mlStatistics&quot;: {object (MlStatistics)},&quot;exportDataStatistics&quot;: {object (ExportDataStatistics)},&quot;externalServiceCosts&quot;: [{object (ExternalServiceCost)}],&quot;biEngineStatistics&quot;: {object (BiEngineStatistics)},&quot;loadQueryStatistics&quot;: {object (LoadQueryStatistics)},&quot;dclTargetTable&quot;: {object (TableReference)},&quot;dclTargetView&quot;: {object (TableReference)},&quot;dclTargetDataset&quot;: {object (DatasetReference)},&quot;searchStatistics&quot;: {object (SearchStatistics)},&quot;vectorSearchStatistics&quot;: {object (VectorSearchStatistics)},&quot;performanceInsights&quot;: {object (PerformanceInsights)},&quot;queryInfo&quot;: {object (QueryInfo)},&quot;sparkStatistics&quot;: {object (SparkStatistics)},&quot;transferredBytes&quot;: string,&quot;materializedViewStatistics&quot;: {object (MaterializedViewStatistics)},&quot;metadataCacheStatistics&quot;: {object (MetadataCacheStatistics)},&quot;incrementalResultStats&quot;: {object (IncrementalResultStats)},&quot;genAiStats&quot;: {object (GenAiStats)},&quot;objectStorageStats&quot;: [{object (ObjectStorageStats)}],// Union field _total_services_sku_slot_ms can be only one of the following:&quot;totalServicesSkuSlotMs&quot;: string// End of list of possible types for union field _total_services_sku_slot_ms.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`queryPlan[]`

` object ( ExplainQueryStage  ` )

Output only. Describes execution plan for the query.

`estimatedBytesProcessed`

`string ( Int64Value format)`

Output only. The original estimate of bytes processed for the job.

`timeline[]`

` object ( QueryTimelineSample  ` )

Output only. Describes a timeline of job execution.

`totalPartitionsProcessed`

`string ( Int64Value format)`

Output only. Total number of partitions processed from all partitioned tables referenced in the job.

`totalBytesProcessed`

`string ( Int64Value format)`

Output only. Total bytes processed for the job.

`totalBytesProcessedAccuracy`

`string`

Output only. For dry-run jobs, totalBytesProcessed is an estimate and this field specifies the accuracy of the estimate. Possible values can be: UNKNOWN: accuracy of the estimate is unknown. PRECISE: estimate is precise. LOWER\_BOUND: estimate is lower bound of what the query would cost. UPPER\_BOUND: estimate is upper bound of what the query would cost.

`totalBytesBilled`

`string ( Int64Value format)`

Output only. If the project is configured to use on-demand pricing, then this field contains the total bytes billed for the job. If the project is configured to use flat-rate pricing, then you are not billed for bytes and this field is informational only.

`billingTier`

`integer`

Output only. Billing tier for the job. This is a BigQuery-specific concept which is not related to the Google Cloud notion of "free tier". The value here is a measure of the query's resource consumption relative to the amount of data scanned. For on-demand queries, the limit is 100, and all queries within this limit are billed at the standard on-demand rates. On-demand queries that exceed this limit will fail with a billingTierLimitExceeded error.

`totalSlotMs`

`string ( Int64Value format)`

Output only. Slot-milliseconds for the job.

` reservationUsage[] (deprecated)  `

` object ( ReservationResourceUsage  ` )

> This item is deprecated\!

Output only. Job resource usage breakdown by reservation. This field reported misleading information and will no longer be populated.

`cacheHit`

`boolean`

Output only. Whether the query result was fetched from the query cache.

`referencedTables[]`

` object ( TableReference  ` )

Output only. Referenced tables for the job.

`referencedRoutines[]`

` object ( RoutineReference  ` )

Output only. Referenced routines for the job.

`referencedPropertyGraphs[]`

` object ( PropertyGraphReference  ` )

Output only. Referenced property graphs for the job. Queries that reference more than 50 property graphs will not have a complete list.

`schema`

` object ( TableSchema  ` )

Output only. The schema of the results. Present only for successful dry run of non-legacy SQL queries.

`numDmlAffectedRows`

`string ( Int64Value format)`

Output only. The number of rows affected by a DML statement. Present only for DML statements INSERT, UPDATE or DELETE.

`dmlStats`

` object ( DmlStats  ` )

Output only. Detailed statistics for DML statements INSERT, UPDATE, DELETE, MERGE or TRUNCATE.

`undeclaredQueryParameters[]`

` object ( QueryParameter  ` )

Output only. GoogleSQL only: list of undeclared query parameters detected during a dry run validation.

`statementType`

`string`

Output only. The type of query statement, if valid. Possible values:

  - `SELECT` : [`SELECT`](https://cloud.google.com/bigquery/docs/reference/standard-sql/query-syntax#select_list) statement.
  - `ASSERT` : [`ASSERT`](https://cloud.google.com/bigquery/docs/reference/standard-sql/debugging-statements#assert) statement.
  - `INSERT` : [`INSERT`](https://cloud.google.com/bigquery/docs/reference/standard-sql/dml-syntax#insert_statement) statement.
  - `UPDATE` : [`UPDATE`](https://cloud.google.com/bigquery/docs/reference/standard-sql/dml-syntax#update_statement) statement.
  - `DELETE` : [`DELETE`](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-manipulation-language) statement.
  - `MERGE` : [`MERGE`](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-manipulation-language) statement.
  - `CREATE_TABLE` : [`CREATE TABLE`](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_table_statement) statement, without `AS SELECT` .
  - `CREATE_TABLE_AS_SELECT` : [`CREATE TABLE AS SELECT`](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_table_statement) statement.
  - `CREATE_VIEW` : [`CREATE VIEW`](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_view_statement) statement.
  - `CREATE_MODEL` : [`CREATE MODEL`](https://cloud.google.com/bigquery-ml/docs/reference/standard-sql/bigqueryml-syntax-create#create_model_statement) statement.
  - `CREATE_MATERIALIZED_VIEW` : [`CREATE MATERIALIZED VIEW`](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_materialized_view_statement) statement.
  - `CREATE_FUNCTION` : [`CREATE FUNCTION`](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_function_statement) statement.
  - `CREATE_TABLE_FUNCTION` : [`CREATE TABLE FUNCTION`](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_table_function_statement) statement.
  - `CREATE_PROCEDURE` : [`CREATE PROCEDURE`](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_procedure) statement.
  - `CREATE_ROW_ACCESS_POLICY` : [`CREATE ROW ACCESS POLICY`](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_row_access_policy_statement) statement.
  - `CREATE_SCHEMA` : [`CREATE SCHEMA`](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_schema_statement) statement.
  - `CREATE_SNAPSHOT_TABLE` : [`CREATE SNAPSHOT TABLE`](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_snapshot_table_statement) statement.
  - `CREATE_SEARCH_INDEX` : [`CREATE SEARCH INDEX`](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_search_index_statement) statement.
  - `DROP_TABLE` : [`DROP TABLE`](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#drop_table_statement) statement.
  - `DROP_EXTERNAL_TABLE` : [`DROP EXTERNAL TABLE`](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#drop_external_table_statement) statement.
  - `DROP_VIEW` : [`DROP VIEW`](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#drop_view_statement) statement.
  - `DROP_MODEL` : [`DROP MODEL`](https://cloud.google.com/bigquery-ml/docs/reference/standard-sql/bigqueryml-syntax-drop-model) statement.
  - `DROP_MATERIALIZED_VIEW` : [`DROP MATERIALIZED VIEW`](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#drop_materialized_view_statement) statement.
  - `DROP_FUNCTION` : [`DROP FUNCTION`](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#drop_function_statement) statement.
  - `DROP_TABLE_FUNCTION` : [`DROP TABLE FUNCTION`](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#drop_table_function) statement.
  - `DROP_PROCEDURE` : [`DROP PROCEDURE`](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#drop_procedure_statement) statement.
  - `DROP_SEARCH_INDEX` : [`DROP SEARCH INDEX`](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#drop_search_index) statement.
  - `DROP_SCHEMA` : [`DROP SCHEMA`](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#drop_schema_statement) statement.
  - `DROP_SNAPSHOT_TABLE` : [`DROP SNAPSHOT TABLE`](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#drop_snapshot_table_statement) statement.
  - `DROP_ROW_ACCESS_POLICY` : [`DROP [ALL] ROW ACCESS POLICY|POLICIES`](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#drop_row_access_policy_statement) statement.
  - `ALTER_TABLE` : [`ALTER TABLE`](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#alter_table_set_options_statement) statement.
  - `ALTER_VIEW` : [`ALTER VIEW`](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#alter_view_set_options_statement) statement.
  - `ALTER_MATERIALIZED_VIEW` : [`ALTER MATERIALIZED VIEW`](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#alter_materialized_view_set_options_statement) statement.
  - `ALTER_SCHEMA` : [`ALTER SCHEMA`](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#alter_schema_set_options_statement) statement.
  - `SCRIPT` : [`SCRIPT`](https://cloud.google.com/bigquery/docs/reference/standard-sql/procedural-language) .
  - `TRUNCATE_TABLE` : [`TRUNCATE TABLE`](https://cloud.google.com/bigquery/docs/reference/standard-sql/dml-syntax#truncate_table_statement) statement.
  - `CREATE_EXTERNAL_TABLE` : [`CREATE EXTERNAL TABLE`](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_external_table_statement) statement.
  - `EXPORT_DATA` : [`EXPORT DATA`](https://cloud.google.com/bigquery/docs/reference/standard-sql/other-statements#export_data_statement) statement.
  - `EXPORT_MODEL` : [`EXPORT MODEL`](https://cloud.google.com/bigquery-ml/docs/reference/standard-sql/bigqueryml-syntax-export-model) statement.
  - `LOAD_DATA` : [`LOAD DATA`](https://cloud.google.com/bigquery/docs/reference/standard-sql/other-statements#load_data_statement) statement.
  - `CALL` : [`CALL`](https://cloud.google.com/bigquery/docs/reference/standard-sql/procedural-language#call) statement.

`ddlOperationPerformed`

`string`

Output only. The DDL operation performed, possibly dependent on the pre-existence of the DDL target.

`ddlTargetTable`

` object ( TableReference  ` )

Output only. The DDL target table. Present only for CREATE/DROP TABLE/VIEW and DROP ALL ROW ACCESS POLICIES queries.

`ddlDestinationTable`

` object ( TableReference  ` )

Output only. The table after rename. Present only for ALTER TABLE RENAME TO query.

`ddlTargetRowAccessPolicy`

` object ( RowAccessPolicyReference  ` )

Output only. The DDL target row access policy. Present only for CREATE/DROP ROW ACCESS POLICY queries.

`ddlAffectedRowAccessPolicyCount`

`string ( Int64Value format)`

Output only. The number of row access policies affected by a DDL statement. Present only for DROP ALL ROW ACCESS POLICIES queries.

`ddlTargetRoutine`

` object ( RoutineReference  ` )

Output only. \[Beta\] The DDL target routine. Present only for CREATE/DROP FUNCTION/PROCEDURE queries.

`ddlTargetDataset`

` object ( DatasetReference  ` )

Output only. The DDL target dataset. Present only for CREATE/ALTER/DROP SCHEMA(dataset) queries.

`mlStatistics`

` object ( MlStatistics  ` )

Output only. Statistics of a BigQuery ML training job.

`exportDataStatistics`

` object ( ExportDataStatistics  ` )

Output only. Stats for EXPORT DATA statement.

`externalServiceCosts[]`

` object ( ExternalServiceCost  ` )

Output only. Job cost breakdown as bigquery internal cost and external service costs.

`biEngineStatistics`

` object ( BiEngineStatistics  ` )

Output only. BI Engine specific Statistics.

`loadQueryStatistics`

` object ( LoadQueryStatistics  ` )

Output only. Statistics for a LOAD query.

`dclTargetTable`

` object ( TableReference  ` )

Output only. Referenced table for DCL statement.

`dclTargetView`

` object ( TableReference  ` )

Output only. Referenced view for DCL statement.

`dclTargetDataset`

` object ( DatasetReference  ` )

Output only. Referenced dataset for DCL statement.

`searchStatistics`

` object ( SearchStatistics  ` )

Output only. Search query specific statistics.

`vectorSearchStatistics`

` object ( VectorSearchStatistics  ` )

Output only. Vector Search query specific statistics.

`performanceInsights`

` object ( PerformanceInsights  ` )

Output only. Performance insights.

`queryInfo`

` object ( QueryInfo  ` )

Output only. Query optimization information for a QUERY job.

`sparkStatistics`

` object ( SparkStatistics  ` )

Output only. Statistics of a Spark procedure job.

`transferredBytes`

`string ( Int64Value format)`

Output only. Total bytes transferred for BigQuery Omni queries from the remote cloud back to Google Cloud. This tracks data movement over Google-managed connections (like query results). It doesn't include input data read from the external data lake (for example, S3) because that data stays within the remote cloud.

`materializedViewStatistics`

` object ( MaterializedViewStatistics  ` )

Output only. Statistics of materialized views of a query job.

`metadataCacheStatistics`

` object ( MetadataCacheStatistics  ` )

Output only. Statistics of metadata cache usage in a query for BigLake tables.

`incrementalResultStats`

` object ( IncrementalResultStats  ` )

Output only. Statistics related to incremental query results, if enabled for the query. This feature is not yet available.

`genAiStats`

` object ( GenAiStats  ` )

Output only. Statistics related to GenAI usage in the query.

`objectStorageStats[]`

` object ( ObjectStorageStats  ` )

Output only. Storage and caching statistics per cloud provider for queries over object storage.

Union field `_total_services_sku_slot_ms` .

`_total_services_sku_slot_ms` can be only one of the following:

`totalServicesSkuSlotMs`

`string ( int64 format)`

Output only. Total slot milliseconds for the job that ran on external services and billed on the services SKU. This field is only populated for jobs that have external service costs, and is the total of the usage for costs whose billing method is `"SERVICES_SKU"` .

### ExplainQueryStage

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;id&quot;: string,&quot;startMs&quot;: string,&quot;endMs&quot;: string,&quot;inputStages&quot;: [string],&quot;waitRatioAvg&quot;: number,&quot;waitMsAvg&quot;: string,&quot;waitRatioMax&quot;: number,&quot;waitMsMax&quot;: string,&quot;readRatioAvg&quot;: number,&quot;readMsAvg&quot;: string,&quot;readRatioMax&quot;: number,&quot;readMsMax&quot;: string,&quot;computeRatioAvg&quot;: number,&quot;computeMsAvg&quot;: string,&quot;computeRatioMax&quot;: number,&quot;computeMsMax&quot;: string,&quot;writeRatioAvg&quot;: number,&quot;writeMsAvg&quot;: string,&quot;writeRatioMax&quot;: number,&quot;writeMsMax&quot;: string,&quot;shuffleOutputBytes&quot;: string,&quot;shuffleOutputBytesSpilled&quot;: string,&quot;recordsRead&quot;: string,&quot;recordsWritten&quot;: string,&quot;parallelInputs&quot;: string,&quot;completedParallelInputs&quot;: string,&quot;status&quot;: string,&quot;steps&quot;: [{object (ExplainQueryStep)}],&quot;slotMs&quot;: string,&quot;computeMode&quot;: enum (ComputeMode)}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`name`

`string`

Human-readable name for the stage.

`id`

`string ( Int64Value format)`

Unique ID for the stage within the plan.

`startMs`

`string ( int64 format)`

Stage start time represented as milliseconds since the epoch.

`endMs`

`string ( int64 format)`

Stage end time represented as milliseconds since the epoch.

`inputStages[]`

`string ( int64 format)`

IDs for stages that are inputs to this stage.

`waitRatioAvg`

`number`

Relative amount of time the average shard spent waiting to be scheduled.

`waitMsAvg`

`string ( Int64Value format)`

Milliseconds the average shard spent waiting to be scheduled.

`waitRatioMax`

`number`

Relative amount of time the slowest shard spent waiting to be scheduled.

`waitMsMax`

`string ( Int64Value format)`

Milliseconds the slowest shard spent waiting to be scheduled.

`readRatioAvg`

`number`

Relative amount of time the average shard spent reading input.

`readMsAvg`

`string ( Int64Value format)`

Milliseconds the average shard spent reading input.

`readRatioMax`

`number`

Relative amount of time the slowest shard spent reading input.

`readMsMax`

`string ( Int64Value format)`

Milliseconds the slowest shard spent reading input.

`computeRatioAvg`

`number`

Relative amount of time the average shard spent on CPU-bound tasks.

`computeMsAvg`

`string ( Int64Value format)`

Milliseconds the average shard spent on CPU-bound tasks.

`computeRatioMax`

`number`

Relative amount of time the slowest shard spent on CPU-bound tasks.

`computeMsMax`

`string ( Int64Value format)`

Milliseconds the slowest shard spent on CPU-bound tasks.

`writeRatioAvg`

`number`

Relative amount of time the average shard spent on writing output.

`writeMsAvg`

`string ( Int64Value format)`

Milliseconds the average shard spent on writing output.

`writeRatioMax`

`number`

Relative amount of time the slowest shard spent on writing output.

`writeMsMax`

`string ( Int64Value format)`

Milliseconds the slowest shard spent on writing output.

`shuffleOutputBytes`

`string ( Int64Value format)`

Total number of bytes written to shuffle.

`shuffleOutputBytesSpilled`

`string ( Int64Value format)`

Total number of bytes written to shuffle and spilled to disk.

`recordsRead`

`string ( Int64Value format)`

Number of records read into the stage.

`recordsWritten`

`string ( Int64Value format)`

Number of records written by the stage.

`parallelInputs`

`string ( Int64Value format)`

Number of parallel input segments to be processed

`completedParallelInputs`

`string ( Int64Value format)`

Number of parallel input segments completed.

`status`

`string`

Current status for this stage.

`steps[]`

` object ( ExplainQueryStep  ` )

List of operations within the stage in dependency order (approximately chronological).

`slotMs`

`string ( Int64Value format)`

Slot-milliseconds used by the stage.

`computeMode`

` enum ( ComputeMode  ` )

Output only. Compute mode for this stage.

### ExplainQueryStep

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;kind&quot;: string,
  &quot;substeps&quot;: [
    string
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`kind`

`string`

Machine-readable operation type.

`substeps[]`

`string`

Human-readable description of the step(s).

### QueryTimelineSample

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;elapsedMs&quot;: string,
  &quot;totalSlotMs&quot;: string,
  &quot;pendingUnits&quot;: string,
  &quot;completedUnits&quot;: string,
  &quot;activeUnits&quot;: string,
  &quot;shuffleRamUsageRatio&quot;: number,
  &quot;estimatedRunnableUnits&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`elapsedMs`

`string ( Int64Value format)`

Milliseconds elapsed since the start of query execution.

`totalSlotMs`

`string ( Int64Value format)`

Cumulative slot-ms consumed by the query.

`pendingUnits`

`string ( Int64Value format)`

Total units of work remaining for the query. This number can be revised (increased or decreased) while the query is running.

`completedUnits`

`string ( Int64Value format)`

Total parallel units of work completed by this query.

`activeUnits`

`string ( Int64Value format)`

Total number of active workers. This does not correspond directly to slot usage. This is the largest value observed since the last sample.

`shuffleRamUsageRatio`

`number`

Total shuffle usage ratio in shuffle RAM per reservation of this query. This will be provided for reservation customers only.

`estimatedRunnableUnits`

`string ( Int64Value format)`

Units of work that can be scheduled immediately. Providing additional slots for these units of work will accelerate the query, if no other query in the reservation needs additional slots.

### ReservationResourceUsage

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;name&quot;: string,
  &quot;slotMs&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`name`

`string`

Reservation name or "unreserved" for on-demand resource usage and multi-statement queries.

`slotMs`

`string ( Int64Value format)`

Total slot milliseconds used by the reservation for a particular job.

### RoutineReference

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;projectId&quot;: string,
  &quot;datasetId&quot;: string,
  &quot;routineId&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`projectId`

`string`

Required. The ID of the project containing this routine.

`datasetId`

`string`

Required. The ID of the dataset containing this routine.

`routineId`

`string`

Required. The ID of the routine. The ID must contain only letters (a-z, A-Z), numbers (0-9), or underscores (\_). The maximum length is 256 characters.

### PropertyGraphReference

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;projectId&quot;: string,
  &quot;datasetId&quot;: string,
  &quot;propertyGraphId&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`projectId`

`string`

Required. The ID of the project containing this property graph.

`datasetId`

`string`

Required. The ID of the dataset containing this property graph.

`propertyGraphId`

`string`

Required. The ID of the property graph. The ID must contain only letters (a-z, A-Z), numbers (0-9), or underscores (\_). The maximum length is 256 characters.

### DmlStats

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;insertedRowCount&quot;: string,&quot;deletedRowCount&quot;: string,&quot;updatedRowCount&quot;: string,&quot;dmlMode&quot;: enum (DmlMode),&quot;fineGrainedDmlUnusedReason&quot;: enum (FineGrainedDmlUnusedReason)}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`insertedRowCount`

`string ( Int64Value format)`

Output only. Number of inserted Rows. Populated by DML INSERT and MERGE statements

`deletedRowCount`

`string ( Int64Value format)`

Output only. Number of deleted Rows. populated by DML DELETE, MERGE and TRUNCATE statements.

`updatedRowCount`

`string ( Int64Value format)`

Output only. Number of updated Rows. Populated by DML UPDATE and MERGE statements.

`dmlMode`

` enum ( DmlMode  ` )

Output only. DML mode used.

`fineGrainedDmlUnusedReason`

` enum ( FineGrainedDmlUnusedReason  ` )

Output only. Reason for disabling fine-grained DML if applicable.

### RowAccessPolicyReference

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;projectId&quot;: string,
  &quot;datasetId&quot;: string,
  &quot;tableId&quot;: string,
  &quot;policyId&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`projectId`

`string`

Required. The ID of the project containing this row access policy.

`datasetId`

`string`

Required. The ID of the dataset containing this row access policy.

`tableId`

`string`

Required. The ID of the table containing this row access policy.

`policyId`

`string`

Required. The ID of the row access policy. The ID must contain only letters (a-z, A-Z), numbers (0-9), or underscores (\_). The maximum length is 256 characters.

### MlStatistics

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;maxIterations&quot;: string,&quot;iterationResults&quot;: [{object (IterationResult)}],&quot;modelType&quot;: enum (ModelType),&quot;trainingType&quot;: enum (TrainingType),&quot;hparamTrials&quot;: [{object (HparamTuningTrial)}]}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`maxIterations`

`string ( int64 format)`

Output only. Maximum number of iterations specified as max\_iterations in the 'CREATE MODEL' query. The actual number of iterations may be less than this number due to early stop.

`iterationResults[]`

` object ( IterationResult  ` )

Results for all completed iterations. Empty for [hyperparameter tuning jobs](https://cloud.google.com/bigquery-ml/docs/reference/standard-sql/bigqueryml-syntax-hp-tuning-overview) .

`modelType`

` enum ( ModelType  ` )

Output only. The type of the model that is being trained.

`trainingType`

` enum ( TrainingType  ` )

Output only. Training type of the job.

`hparamTrials[]`

` object ( HparamTuningTrial  ` )

Output only. Trials of a [hyperparameter tuning job](https://cloud.google.com/bigquery-ml/docs/reference/standard-sql/bigqueryml-syntax-hp-tuning-overview) sorted by trial\_id.

### IterationResult

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;index&quot;: integer,&quot;durationMs&quot;: string,&quot;trainingLoss&quot;: number,&quot;evalLoss&quot;: number,&quot;learnRate&quot;: number,&quot;clusterInfos&quot;: [{object (ClusterInfo)}],&quot;arimaResult&quot;: {object (ArimaResult)},&quot;principalComponentInfos&quot;: [{object (PrincipalComponentInfo)}]}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`index`

`integer`

Index of the iteration, 0 based.

`durationMs`

`string ( Int64Value format)`

Time taken to run the iteration in milliseconds.

`trainingLoss`

`number`

Loss computed on the training data at the end of iteration.

`evalLoss`

`number`

Loss computed on the eval data at the end of iteration.

`learnRate`

`number`

Learn rate used for this iteration.

`clusterInfos[]`

` object ( ClusterInfo  ` )

Information about top clusters for clustering models.

`arimaResult`

` object ( ArimaResult  ` )

Arima result.

`principalComponentInfos[]`

` object ( PrincipalComponentInfo  ` )

The information of the principal components.

### ClusterInfo

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;centroidId&quot;: string,
  &quot;clusterRadius&quot;: number,
  &quot;clusterSize&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`centroidId`

`string ( int64 format)`

Centroid id.

`clusterRadius`

`number`

Cluster radius, the average distance from centroid to each point assigned to the cluster.

`clusterSize`

`string ( Int64Value format)`

Cluster size, the total number of points assigned to the cluster.

### ArimaResult

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;arimaModelInfo&quot;: [{object (ArimaModelInfo)}],&quot;seasonalPeriods&quot;: [enum (SeasonalPeriodType)]}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`arimaModelInfo[]`

` object ( ArimaModelInfo  ` )

This message is repeated because there are multiple arima models fitted in auto-arima. For non-auto-arima model, its size is one.

`seasonalPeriods[]`

` enum ( SeasonalPeriodType  ` )

Seasonal periods. Repeated because multiple periods are supported for one time series.

### ArimaModelInfo

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;nonSeasonalOrder&quot;: {object (ArimaOrder)},&quot;arimaCoefficients&quot;: {object (ArimaCoefficients)},&quot;arimaFittingMetrics&quot;: {object (ArimaFittingMetrics)},&quot;hasDrift&quot;: boolean,&quot;timeSeriesId&quot;: string,&quot;timeSeriesIds&quot;: [string],&quot;seasonalPeriods&quot;: [enum (SeasonalPeriodType)],&quot;hasHolidayEffect&quot;: boolean,&quot;hasSpikesAndDips&quot;: boolean,&quot;hasStepChanges&quot;: boolean}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`nonSeasonalOrder`

` object ( ArimaOrder  ` )

Non-seasonal order.

`arimaCoefficients`

` object ( ArimaCoefficients  ` )

Arima coefficients.

`arimaFittingMetrics`

` object ( ArimaFittingMetrics  ` )

Arima fitting metrics.

`hasDrift`

`boolean`

Whether Arima model fitted with drift or not. It is always false when d is not 1.

`timeSeriesId`

`string`

The time\_series\_id value for this time series. It will be one of the unique values from the time\_series\_id\_column specified during ARIMA model training. Only present when time\_series\_id\_column training option was used.

`timeSeriesIds[]`

`string`

The tuple of time\_series\_ids identifying this time series. It will be one of the unique tuples of values present in the time\_series\_id\_columns specified during ARIMA model training. Only present when time\_series\_id\_columns training option was used and the order of values here are same as the order of time\_series\_id\_columns.

`seasonalPeriods[]`

` enum ( SeasonalPeriodType  ` )

Seasonal periods. Repeated because multiple periods are supported for one time series.

`hasHolidayEffect`

`boolean`

If true, holiday\_effect is a part of time series decomposition result.

`hasSpikesAndDips`

`boolean`

If true, spikes\_and\_dips is a part of time series decomposition result.

`hasStepChanges`

`boolean`

If true, step\_changes is a part of time series decomposition result.

### ArimaOrder

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;p&quot;: string,
  &quot;d&quot;: string,
  &quot;q&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`p`

`string ( Int64Value format)`

Order of the autoregressive part.

`d`

`string ( Int64Value format)`

Order of the differencing part.

`q`

`string ( Int64Value format)`

Order of the moving-average part.

### ArimaCoefficients

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;autoRegressiveCoefficients&quot;: [
    number
  ],
  &quot;movingAverageCoefficients&quot;: [
    number
  ],
  &quot;interceptCoefficient&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`autoRegressiveCoefficients[]`

`number`

Auto-regressive coefficients, an array of double.

`movingAverageCoefficients[]`

`number`

Moving-average coefficients, an array of double.

`interceptCoefficient`

`number`

Intercept coefficient, just a double not an array.

### ArimaFittingMetrics

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;logLikelihood&quot;: number,
  &quot;aic&quot;: number,
  &quot;variance&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`logLikelihood`

`number`

Log-likelihood.

`aic`

`number`

AIC.

`variance`

`number`

Variance.

### PrincipalComponentInfo

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;principalComponentId&quot;: string,
  &quot;explainedVariance&quot;: number,
  &quot;explainedVarianceRatio&quot;: number,
  &quot;cumulativeExplainedVarianceRatio&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`principalComponentId`

`string ( Int64Value format)`

Id of the principal component.

`explainedVariance`

`number`

Explained variance by this principal component, which is simply the eigenvalue.

`explainedVarianceRatio`

`number`

Explained\_variance over the total explained variance.

`cumulativeExplainedVarianceRatio`

`number`

The explained\_variance is pre-ordered in the descending order to compute the cumulative explained variance ratio.

### HparamTuningTrial

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;trialId&quot;: string,&quot;startTimeMs&quot;: string,&quot;endTimeMs&quot;: string,&quot;hparams&quot;: {object (TrainingOptions)},&quot;evaluationMetrics&quot;: {object (EvaluationMetrics)},&quot;status&quot;: enum (TrialStatus),&quot;errorMessage&quot;: string,&quot;trainingLoss&quot;: number,&quot;evalLoss&quot;: number,&quot;hparamTuningEvaluationMetrics&quot;: {object (EvaluationMetrics)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`trialId`

`string ( int64 format)`

1-based index of the trial.

`startTimeMs`

`string ( int64 format)`

Starting time of the trial.

`endTimeMs`

`string ( int64 format)`

Ending time of the trial.

`hparams`

` object ( TrainingOptions  ` )

The hyperprameters selected for this trial.

`evaluationMetrics`

` object ( EvaluationMetrics  ` )

Evaluation metrics of this trial calculated on the test data. Empty in Job API.

`status`

` enum ( TrialStatus  ` )

The status of the trial.

`errorMessage`

`string`

Error message for FAILED and INFEASIBLE trial.

`trainingLoss`

`number`

Loss computed on the training data at the end of trial.

`evalLoss`

`number`

Loss computed on the eval data at the end of trial.

`hparamTuningEvaluationMetrics`

` object ( EvaluationMetrics  ` )

Hyperparameter tuning evaluation metrics of this trial calculated on the eval data. Unlike evaluation\_metrics, only the fields corresponding to the hparam\_tuning\_objectives are set.

### TrainingOptions

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;maxIterations&quot;: string,&quot;lossType&quot;: enum (LossType),&quot;learnRate&quot;: number,&quot;l1Regularization&quot;: number,&quot;l2Regularization&quot;: number,&quot;minRelativeProgress&quot;: number,&quot;warmStart&quot;: boolean,&quot;earlyStop&quot;: boolean,&quot;inputLabelColumns&quot;: [string],&quot;dataSplitMethod&quot;: enum (DataSplitMethod),&quot;dataSplitEvalFraction&quot;: number,&quot;dataSplitColumn&quot;: string,&quot;learnRateStrategy&quot;: enum (LearnRateStrategy),&quot;initialLearnRate&quot;: number,&quot;labelClassWeights&quot;: {string: number,...},&quot;userColumn&quot;: string,&quot;itemColumn&quot;: string,&quot;distanceType&quot;: enum (DistanceType),&quot;numClusters&quot;: string,&quot;modelUri&quot;: string,&quot;optimizationStrategy&quot;: enum (OptimizationStrategy),&quot;hiddenUnits&quot;: [string],&quot;batchSize&quot;: string,&quot;dropout&quot;: number,&quot;maxTreeDepth&quot;: string,&quot;subsample&quot;: number,&quot;minSplitLoss&quot;: number,&quot;boosterType&quot;: enum (BoosterType),&quot;numParallelTree&quot;: string,&quot;dartNormalizeType&quot;: enum (DartNormalizeType),&quot;treeMethod&quot;: enum (TreeMethod),&quot;minTreeChildWeight&quot;: string,&quot;colsampleBytree&quot;: number,&quot;colsampleBylevel&quot;: number,&quot;colsampleBynode&quot;: number,&quot;numFactors&quot;: string,&quot;feedbackType&quot;: enum (FeedbackType),&quot;walsAlpha&quot;: number,&quot;kmeansInitializationMethod&quot;: enum (KmeansInitializationMethod),&quot;kmeansInitializationColumn&quot;: string,&quot;timeSeriesTimestampColumn&quot;: string,&quot;timeSeriesDataColumn&quot;: string,&quot;autoArima&quot;: boolean,&quot;nonSeasonalOrder&quot;: {object (ArimaOrder)},&quot;dataFrequency&quot;: enum (DataFrequency),&quot;calculatePValues&quot;: boolean,&quot;includeDrift&quot;: boolean,&quot;holidayRegion&quot;: enum (HolidayRegion),&quot;holidayRegions&quot;: [enum (HolidayRegion)],&quot;timeSeriesIdColumn&quot;: string,&quot;timeSeriesIdColumns&quot;: [string],&quot;forecastLimitLowerBound&quot;: number,&quot;forecastLimitUpperBound&quot;: number,&quot;horizon&quot;: string,&quot;autoArimaMaxOrder&quot;: string,&quot;autoArimaMinOrder&quot;: string,&quot;numTrials&quot;: string,&quot;maxParallelTrials&quot;: string,&quot;hparamTuningObjectives&quot;: [enum (HparamTuningObjective)],&quot;decomposeTimeSeries&quot;: boolean,&quot;cleanSpikesAndDips&quot;: boolean,&quot;adjustStepChanges&quot;: boolean,&quot;enableGlobalExplain&quot;: boolean,&quot;sampledShapleyNumPaths&quot;: string,&quot;integratedGradientsNumSteps&quot;: string,&quot;categoryEncodingMethod&quot;: enum (EncodingMethod),&quot;tfVersion&quot;: string,&quot;colorSpace&quot;: enum (ColorSpace),&quot;instanceWeightColumn&quot;: string,&quot;trendSmoothingWindowSize&quot;: string,&quot;timeSeriesLengthFraction&quot;: number,&quot;minTimeSeriesLength&quot;: string,&quot;maxTimeSeriesLength&quot;: string,&quot;xgboostVersion&quot;: string,&quot;approxGlobalFeatureContrib&quot;: boolean,&quot;fitIntercept&quot;: boolean,&quot;numPrincipalComponents&quot;: string,&quot;pcaExplainedVarianceRatio&quot;: number,&quot;scaleFeatures&quot;: boolean,&quot;pcaSolver&quot;: enum (PcaSolver),&quot;autoClassWeights&quot;: boolean,&quot;activationFn&quot;: string,&quot;optimizer&quot;: string,&quot;budgetHours&quot;: number,&quot;standardizeFeatures&quot;: boolean,&quot;l1RegActivation&quot;: number,&quot;modelRegistry&quot;: enum (ModelRegistry),&quot;vertexAiModelVersionAliases&quot;: [string],&quot;dimensionIdColumns&quot;: [string],&quot;reservationAffinityValues&quot;: [string],// Union field _contribution_metric can be only one of the following:&quot;contributionMetric&quot;: string// End of list of possible types for union field _contribution_metric.// Union field _is_test_column can be only one of the following:&quot;isTestColumn&quot;: string// End of list of possible types for union field _is_test_column.// Union field _min_apriori_support can be only one of the following:&quot;minAprioriSupport&quot;: number// End of list of possible types for union field _min_apriori_support.// Union field external_model_id can be only one of the following:&quot;huggingFaceModelId&quot;: string,&quot;modelGardenModelName&quot;: string// End of list of possible types for union field external_model_id.// Union field _endpoint_idle_ttl can be only one of the following:&quot;endpointIdleTtl&quot;: string// End of list of possible types for union field _endpoint_idle_ttl.// Union field _machine_type can be only one of the following:&quot;machineType&quot;: string// End of list of possible types for union field _machine_type.// Union field _min_replica_count can be only one of the following:&quot;minReplicaCount&quot;: string// End of list of possible types for union field _min_replica_count.// Union field _max_replica_count can be only one of the following:&quot;maxReplicaCount&quot;: string// End of list of possible types for union field _max_replica_count.// Union field _reservation_affinity_type can be only one of the following:&quot;reservationAffinityType&quot;: enum (ReservationAffinityType)// End of list of possible types for union field _reservation_affinity_type.// Union field _reservation_affinity_key can be only one of the following:&quot;reservationAffinityKey&quot;: string// End of list of possible types for union field _reservation_affinity_key.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`maxIterations`

`string ( int64 format)`

The maximum number of iterations in training. Used only for iterative training algorithms.

`lossType`

` enum ( LossType  ` )

Type of loss function used during training run.

`learnRate`

`number`

Learning rate in training. Used only for iterative training algorithms.

`l1Regularization`

`number`

L1 regularization coefficient.

`l2Regularization`

`number`

L2 regularization coefficient.

`minRelativeProgress`

`number`

When early\_stop is true, stops training when accuracy improvement is less than 'min\_relative\_progress'. Used only for iterative training algorithms.

`warmStart`

`boolean`

Whether to train a model from the last checkpoint.

`earlyStop`

`boolean`

Whether to stop early when the loss doesn't improve significantly any more (compared to min\_relative\_progress). Used only for iterative training algorithms.

`inputLabelColumns[]`

`string`

Name of input label columns in training data.

`dataSplitMethod`

` enum ( DataSplitMethod  ` )

The data split type for training and evaluation, e.g. RANDOM.

`dataSplitEvalFraction`

`number`

The fraction of evaluation data over the whole input data. The rest of data will be used as training data. The format should be double. Accurate to two decimal places. Default value is 0.2.

`dataSplitColumn`

`string`

The column to split data with. This column won't be used as a feature. 1. When data\_split\_method is CUSTOM, the corresponding column should be boolean. The rows with true value tag are eval data, and the false are training data. 2. When data\_split\_method is SEQ, the first DATA\_SPLIT\_EVAL\_FRACTION rows (from smallest to largest) in the corresponding column are used as training data, and the rest are eval data. It respects the order in Orderable data types: <https://cloud.google.com/bigquery/docs/reference/standard-sql/data-types#data_type_properties>

`learnRateStrategy`

` enum ( LearnRateStrategy  ` )

The strategy to determine learn rate for the current iteration.

`initialLearnRate`

`number`

Specifies the initial learning rate for the line search learn rate strategy.

`labelClassWeights`

`map (key: string, value: number)`

Weights associated with each label class, for rebalancing the training data. Only applicable for classification models.

An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .

`userColumn`

`string`

User column specified for matrix factorization models.

`itemColumn`

`string`

Item column specified for matrix factorization models.

`distanceType`

` enum ( DistanceType  ` )

Distance type for clustering models.

`numClusters`

`string ( int64 format)`

Number of clusters for clustering models.

`modelUri`

`string`

Google Cloud Storage URI from which the model was imported. Only applicable for imported models.

`optimizationStrategy`

` enum ( OptimizationStrategy  ` )

Optimization strategy for training linear regression models.

`hiddenUnits[]`

`string ( int64 format)`

Hidden units for dnn models.

`batchSize`

`string ( int64 format)`

Batch size for dnn models.

`dropout`

`number`

Dropout probability for dnn models.

`maxTreeDepth`

`string ( int64 format)`

Maximum depth of a tree for boosted tree models.

`subsample`

`number`

Subsample fraction of the training data to grow tree to prevent overfitting for boosted tree models.

`minSplitLoss`

`number`

Minimum split loss for boosted tree models.

`boosterType`

` enum ( BoosterType  ` )

Booster type for boosted tree models.

`numParallelTree`

`string ( Int64Value format)`

Number of parallel trees constructed during each iteration for boosted tree models.

`dartNormalizeType`

` enum ( DartNormalizeType  ` )

Type of normalization algorithm for boosted tree models using dart booster.

`treeMethod`

` enum ( TreeMethod  ` )

Tree construction algorithm for boosted tree models.

`minTreeChildWeight`

`string ( Int64Value format)`

Minimum sum of instance weight needed in a child for boosted tree models.

`colsampleBytree`

`number`

Subsample ratio of columns when constructing each tree for boosted tree models.

`colsampleBylevel`

`number`

Subsample ratio of columns for each level for boosted tree models.

`colsampleBynode`

`number`

Subsample ratio of columns for each node(split) for boosted tree models.

`numFactors`

`string ( int64 format)`

Num factors specified for matrix factorization models.

`feedbackType`

` enum ( FeedbackType  ` )

Feedback type that specifies which algorithm to run for matrix factorization.

`walsAlpha`

`number`

Hyperparameter for matrix factoration when implicit feedback type is specified.

`kmeansInitializationMethod`

` enum ( KmeansInitializationMethod  ` )

The method used to initialize the centroids for kmeans algorithm.

`kmeansInitializationColumn`

`string`

The column used to provide the initial centroids for kmeans algorithm when kmeans\_initialization\_method is CUSTOM.

`timeSeriesTimestampColumn`

`string`

Column to be designated as time series timestamp for ARIMA model.

`timeSeriesDataColumn`

`string`

Column to be designated as time series data for ARIMA model.

`autoArima`

`boolean`

Whether to enable auto ARIMA or not.

`nonSeasonalOrder`

` object ( ArimaOrder  ` )

A specification of the non-seasonal part of the ARIMA model: the three components (p, d, q) are the AR order, the degree of differencing, and the MA order.

`dataFrequency`

` enum ( DataFrequency  ` )

The data frequency of a time series.

`calculatePValues`

`boolean`

Whether or not p-value test should be computed for this model. Only available for linear and logistic regression models.

`includeDrift`

`boolean`

Include drift when fitting an ARIMA model.

`holidayRegion`

` enum ( HolidayRegion  ` )

The geographical region based on which the holidays are considered in time series modeling. If a valid value is specified, then holiday effects modeling is enabled.

`holidayRegions[]`

` enum ( HolidayRegion  ` )

A list of geographical regions that are used for time series modeling.

`timeSeriesIdColumn`

`string`

The time series id column that was used during ARIMA model training.

`timeSeriesIdColumns[]`

`string`

The time series id columns that were used during ARIMA model training.

`forecastLimitLowerBound`

`number`

The forecast limit lower bound that was used during ARIMA model training with limits. To see more details of the algorithm: <https://otexts.com/fpp2/limits.html>

`forecastLimitUpperBound`

`number`

The forecast limit upper bound that was used during ARIMA model training with limits.

`horizon`

`string ( int64 format)`

The number of periods ahead that need to be forecasted.

`autoArimaMaxOrder`

`string ( int64 format)`

The max value of the sum of non-seasonal p and q.

`autoArimaMinOrder`

`string ( int64 format)`

The min value of the sum of non-seasonal p and q.

`numTrials`

`string ( int64 format)`

Number of trials to run this hyperparameter tuning job.

`maxParallelTrials`

`string ( int64 format)`

Maximum number of trials to run in parallel.

`hparamTuningObjectives[]`

` enum ( HparamTuningObjective  ` )

The target evaluation metrics to optimize the hyperparameters for.

`decomposeTimeSeries`

`boolean`

If true, perform decompose time series and save the results.

`cleanSpikesAndDips`

`boolean`

If true, clean spikes and dips in the input time series.

`adjustStepChanges`

`boolean`

If true, detect step changes and make data adjustment in the input time series.

`enableGlobalExplain`

`boolean`

If true, enable global explanation during training.

`sampledShapleyNumPaths`

`string ( int64 format)`

Number of paths for the sampled Shapley explain method.

`integratedGradientsNumSteps`

`string ( int64 format)`

Number of integral steps for the integrated gradients explain method.

`categoryEncodingMethod`

` enum ( EncodingMethod  ` )

Categorical feature encoding method.

`tfVersion`

`string`

Based on the selected TF version, the corresponding docker image is used to train external models.

`colorSpace`

` enum ( ColorSpace  ` )

Enums for color space, used for processing images in Object Table. See more details at <https://www.tensorflow.org/io/tutorials/colorspace> .

`instanceWeightColumn`

`string`

Name of the instance weight column for training data. This column isn't be used as a feature.

`trendSmoothingWindowSize`

`string ( int64 format)`

Smoothing window size for the trend component. When a positive value is specified, a center moving average smoothing is applied on the history trend. When the smoothing window is out of the boundary at the beginning or the end of the trend, the first element or the last element is padded to fill the smoothing window before the average is applied.

`timeSeriesLengthFraction`

`number`

The fraction of the interpolated length of the time series that's used to model the time series trend component. All of the time points of the time series are used to model the non-trend component. This training option accelerates modeling training without sacrificing much forecasting accuracy. You can use this option with `minTimeSeriesLength` but not with `maxTimeSeriesLength` .

`minTimeSeriesLength`

`string ( int64 format)`

The minimum number of time points in a time series that are used in modeling the trend component of the time series. If you use this option you must also set the `timeSeriesLengthFraction` option. This training option ensures that enough time points are available when you use `timeSeriesLengthFraction` in trend modeling. This is particularly important when forecasting multiple time series in a single query using `timeSeriesIdColumn` . If the total number of time points is less than the `minTimeSeriesLength` value, then the query uses all available time points.

`maxTimeSeriesLength`

`string ( int64 format)`

The maximum number of time points in a time series that can be used in modeling the trend component of the time series. Don't use this option with the `timeSeriesLengthFraction` or `minTimeSeriesLength` options.

`xgboostVersion`

`string`

User-selected XGBoost versions for training of XGBoost models.

`approxGlobalFeatureContrib`

`boolean`

Whether to use approximate feature contribution method in XGBoost model explanation for global explain.

`fitIntercept`

`boolean`

Whether the model should include intercept during model training.

`numPrincipalComponents`

`string ( int64 format)`

Number of principal components to keep in the PCA model. Must be \<= the number of features.

`pcaExplainedVarianceRatio`

`number`

The minimum ratio of cumulative explained variance that needs to be given by the PCA model.

`scaleFeatures`

`boolean`

If true, scale the feature values by dividing the feature standard deviation. Currently only apply to PCA.

`pcaSolver`

` enum ( PcaSolver  ` )

The solver for PCA.

`autoClassWeights`

`boolean`

Whether to calculate class weights automatically based on the popularity of each label.

`activationFn`

`string`

Activation function of the neural nets.

`optimizer`

`string`

Optimizer used for training the neural nets.

`budgetHours`

`number`

Budget in hours for AutoML training.

`standardizeFeatures`

`boolean`

Whether to standardize numerical features. Default to true.

`l1RegActivation`

`number`

L1 regularization coefficient to activations.

`modelRegistry`

` enum ( ModelRegistry  ` )

The model registry.

`vertexAiModelVersionAliases[]`

`string`

The version aliases to apply in Vertex AI model registry. Always overwrite if the version aliases exists in a existing model.

`dimensionIdColumns[]`

`string`

Optional. Names of the columns to slice on. Applies to contribution analysis models.

`reservationAffinityValues[]`

`string`

Corresponds to the label values of a reservation resource used by Vertex AI. This must be the full resource name of the reservation or reservation block.

Union field `_contribution_metric` .

`_contribution_metric` can be only one of the following:

`contributionMetric`

`string`

The contribution metric. Applies to contribution analysis models. Allowed formats supported are for summable and summable ratio contribution metrics. These include expressions such as `SUM(x)` or `SUM(x)/SUM(y)` , where x and y are column names from the base table.

Union field `_is_test_column` .

`_is_test_column` can be only one of the following:

`isTestColumn`

`string`

Name of the column used to determine the rows corresponding to control and test. Applies to contribution analysis models.

Union field `_min_apriori_support` .

`_min_apriori_support` can be only one of the following:

`minAprioriSupport`

`number`

The apriori support minimum. Applies to contribution analysis models.

Union field `external_model_id` . The id that uniquely identifies an external model. `external_model_id` can be only one of the following:

`huggingFaceModelId`

`string`

The id of a Hugging Face model. For example, `google/gemma-2-2b-it` .

`modelGardenModelName`

`string`

The name of a Vertex model garden publisher model. Format is `publishers/{publisher}/models/{model}@{optional_version_id}` .

Union field `_endpoint_idle_ttl` .

`_endpoint_idle_ttl` can be only one of the following:

`endpointIdleTtl`

` string ( Duration  ` format)

The idle TTL of the endpoint before the resources get destroyed. The default value is 6.5 hours.

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

Union field `_machine_type` .

`_machine_type` can be only one of the following:

`machineType`

`string`

The type of the machine used to deploy and serve the model.

Union field `_min_replica_count` .

`_min_replica_count` can be only one of the following:

`minReplicaCount`

`string ( int64 format)`

The minimum number of machine replicas that will be always deployed on an endpoint. This value must be greater than or equal to 1. The default value is 1.

Union field `_max_replica_count` .

`_max_replica_count` can be only one of the following:

`maxReplicaCount`

`string ( int64 format)`

The maximum number of machine replicas that will be deployed on an endpoint. The default value is equal to min\_replica\_count.

Union field `_reservation_affinity_type` .

`_reservation_affinity_type` can be only one of the following:

`reservationAffinityType`

` enum ( ReservationAffinityType  ` )

Specifies the reservation affinity type used to configure a Vertex AI resource. The default value is `NO_RESERVATION` .

Union field `_reservation_affinity_key` .

`_reservation_affinity_key` can be only one of the following:

`reservationAffinityKey`

`string`

Corresponds to the label key of a reservation resource used by Vertex AI. To target a SPECIFIC\_RESERVATION by name, use `compute.googleapis.com/reservation-name` as the key and specify the name of your reservation as its value.

### LabelClassWeightsEntry

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;key&quot;: string,
  &quot;value&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`key`

`string`

`value`

`number`

### Duration

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;seconds&quot;: string,
  &quot;nanos&quot;: integer
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`seconds`

`string ( int64 format)`

Signed seconds of the span of time. Must be from -315,576,000,000 to +315,576,000,000 inclusive. Note: these bounds are computed from: 60 sec/min \* 60 min/hr \* 24 hr/day \* 365.25 days/year \* 10000 years

`nanos`

`integer`

Signed fractions of a second at nanosecond resolution of the span of time. Durations less than one second are represented with a 0 `seconds` field and a positive or negative `nanos` field. For durations of one second or more, a non-zero value for the `nanos` field must be of the same sign as the `seconds` field. Must be from -999,999,999 to +999,999,999 inclusive.

### EvaluationMetrics

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field metrics can be only one of the following:&quot;regressionMetrics&quot;: {object (RegressionMetrics)},&quot;binaryClassificationMetrics&quot;: {object (BinaryClassificationMetrics)},&quot;multiClassClassificationMetrics&quot;: {object (MultiClassClassificationMetrics)},&quot;clusteringMetrics&quot;: {object (ClusteringMetrics)},&quot;rankingMetrics&quot;: {object (RankingMetrics)},&quot;arimaForecastingMetrics&quot;: {object (ArimaForecastingMetrics)},&quot;dimensionalityReductionMetrics&quot;: {object (DimensionalityReductionMetrics)}// End of list of possible types for union field metrics.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `metrics` . Metrics. `metrics` can be only one of the following:

`regressionMetrics`

` object ( RegressionMetrics  ` )

Populated for regression models and explicit feedback type matrix factorization models.

`binaryClassificationMetrics`

` object ( BinaryClassificationMetrics  ` )

Populated for binary classification/classifier models.

`multiClassClassificationMetrics`

` object ( MultiClassClassificationMetrics  ` )

Populated for multi-class classification/classifier models.

`clusteringMetrics`

` object ( ClusteringMetrics  ` )

Populated for clustering models.

`rankingMetrics`

` object ( RankingMetrics  ` )

Populated for implicit feedback type matrix factorization models.

`arimaForecastingMetrics`

` object ( ArimaForecastingMetrics  ` )

Populated for ARIMA models.

`dimensionalityReductionMetrics`

` object ( DimensionalityReductionMetrics  ` )

Evaluation metrics when the model is a dimensionality reduction model, which currently includes PCA.

### RegressionMetrics

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;meanAbsoluteError&quot;: number,
  &quot;meanSquaredError&quot;: number,
  &quot;meanSquaredLogError&quot;: number,
  &quot;medianAbsoluteError&quot;: number,
  &quot;rSquared&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`meanAbsoluteError`

`number`

Mean absolute error.

`meanSquaredError`

`number`

Mean squared error.

`meanSquaredLogError`

`number`

Mean squared log error.

`medianAbsoluteError`

`number`

Median absolute error.

`rSquared`

`number`

R^2 score. This corresponds to r2\_score in ML.EVALUATE.

### BinaryClassificationMetrics

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;aggregateClassificationMetrics&quot;: {object (AggregateClassificationMetrics)},&quot;binaryConfusionMatrixList&quot;: [{object (BinaryConfusionMatrix)}],&quot;positiveLabel&quot;: string,&quot;negativeLabel&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`aggregateClassificationMetrics`

` object ( AggregateClassificationMetrics  ` )

Aggregate classification metrics.

`binaryConfusionMatrixList[]`

` object ( BinaryConfusionMatrix  ` )

Binary confusion matrix at multiple thresholds.

`positiveLabel`

`string`

Label representing the positive class.

`negativeLabel`

`string`

Label representing the negative class.

### AggregateClassificationMetrics

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;precision&quot;: number,
  &quot;recall&quot;: number,
  &quot;accuracy&quot;: number,
  &quot;threshold&quot;: number,
  &quot;f1Score&quot;: number,
  &quot;logLoss&quot;: number,
  &quot;rocAuc&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`precision`

`number`

Precision is the fraction of actual positive predictions that had positive actual labels. For multiclass this is a macro-averaged metric treating each class as a binary classifier.

`recall`

`number`

Recall is the fraction of actual positive labels that were given a positive prediction. For multiclass this is a macro-averaged metric.

`accuracy`

`number`

Accuracy is the fraction of predictions given the correct label. For multiclass this is a micro-averaged metric.

`threshold`

`number`

Threshold at which the metrics are computed. For binary classification models this is the positive class threshold. For multi-class classification models this is the confidence threshold.

`f1Score`

`number`

The F1 score is an average of recall and precision. For multiclass this is a macro-averaged metric.

`logLoss`

`number`

Logarithmic Loss. For multiclass this is a macro-averaged metric.

`rocAuc`

`number`

Area Under a ROC Curve. For multiclass this is a macro-averaged metric.

### BinaryConfusionMatrix

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;positiveClassThreshold&quot;: number,
  &quot;truePositives&quot;: string,
  &quot;falsePositives&quot;: string,
  &quot;trueNegatives&quot;: string,
  &quot;falseNegatives&quot;: string,
  &quot;precision&quot;: number,
  &quot;recall&quot;: number,
  &quot;f1Score&quot;: number,
  &quot;accuracy&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`positiveClassThreshold`

`number`

Threshold value used when computing each of the following metric.

`truePositives`

`string ( Int64Value format)`

Number of true samples predicted as true.

`falsePositives`

`string ( Int64Value format)`

Number of false samples predicted as true.

`trueNegatives`

`string ( Int64Value format)`

Number of true samples predicted as false.

`falseNegatives`

`string ( Int64Value format)`

Number of false samples predicted as false.

`precision`

`number`

The fraction of actual positive predictions that had positive actual labels.

`recall`

`number`

The fraction of actual positive labels that were given a positive prediction.

`f1Score`

`number`

The equally weighted average of recall and precision.

`accuracy`

`number`

The fraction of predictions given the correct label.

### MultiClassClassificationMetrics

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;aggregateClassificationMetrics&quot;: {object (AggregateClassificationMetrics)},&quot;confusionMatrixList&quot;: [{object (ConfusionMatrix)}]}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`aggregateClassificationMetrics`

` object ( AggregateClassificationMetrics  ` )

Aggregate classification metrics.

`confusionMatrixList[]`

` object ( ConfusionMatrix  ` )

Confusion matrix at different thresholds.

### ConfusionMatrix

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;confidenceThreshold&quot;: number,&quot;rows&quot;: [{object (Row)}]}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`confidenceThreshold`

`number`

Confidence threshold used when computing the entries of the confusion matrix.

`rows[]`

` object ( Row  ` )

One row per actual label.

### Row

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;actualLabel&quot;: string,&quot;entries&quot;: [{object (Entry)}]}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`actualLabel`

`string`

The original label of this row.

`entries[]`

` object ( Entry  ` )

Info describing predicted label distribution.

### Entry

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;predictedLabel&quot;: string,
  &quot;itemCount&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`predictedLabel`

`string`

The predicted label. For confidence\_threshold \> 0, we will also add an entry indicating the number of items under the confidence threshold.

`itemCount`

`string ( Int64Value format)`

Number of items being predicted as this label.

### ClusteringMetrics

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;daviesBouldinIndex&quot;: number,&quot;meanSquaredDistance&quot;: number,&quot;clusters&quot;: [{object (Cluster)}]}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`daviesBouldinIndex`

`number`

Davies-Bouldin index.

`meanSquaredDistance`

`number`

Mean of squared distances between each sample to its cluster centroid.

`clusters[]`

` object ( Cluster  ` )

Information for all clusters.

### Cluster

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;centroidId&quot;: string,&quot;featureValues&quot;: [{object (FeatureValue)}],&quot;count&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`centroidId`

`string ( int64 format)`

Centroid id.

`featureValues[]`

` object ( FeatureValue  ` )

Values of highly variant features for this cluster.

`count`

`string ( Int64Value format)`

Count of training data rows that were assigned to this cluster.

### FeatureValue

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;featureColumn&quot;: string,// Union field value can be only one of the following:&quot;numericalValue&quot;: number,&quot;categoricalValue&quot;: {object (CategoricalValue)}// End of list of possible types for union field value.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`featureColumn`

`string`

The feature column name.

Union field `value` . Value. `value` can be only one of the following:

`numericalValue`

`number`

The numerical feature value. This is the centroid value for this feature.

`categoricalValue`

` object ( CategoricalValue  ` )

The categorical feature value.

### CategoricalValue

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;categoryCounts&quot;: [{object (CategoryCount)}]}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`categoryCounts[]`

` object ( CategoryCount  ` )

Counts of all categories for the categorical feature. If there are more than ten categories, we return top ten (by count) and return one more CategoryCount with category "\_OTHER\_" and count as aggregate counts of remaining categories.

### CategoryCount

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;category&quot;: string,
  &quot;count&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`category`

`string`

The name of category.

`count`

`string ( Int64Value format)`

The count of training samples matching the category within the cluster.

### RankingMetrics

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;meanAveragePrecision&quot;: number,
  &quot;meanSquaredError&quot;: number,
  &quot;normalizedDiscountedCumulativeGain&quot;: number,
  &quot;averageRank&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`meanAveragePrecision`

`number`

Calculates a precision per user for all the items by ranking them and then averages all the precisions across all the users.

`meanSquaredError`

`number`

Similar to the mean squared error computed in regression and explicit recommendation models except instead of computing the rating directly, the output from evaluate is computed against a preference which is 1 or 0 depending on if the rating exists or not.

`normalizedDiscountedCumulativeGain`

`number`

A metric to determine the goodness of a ranking calculated from the predicted confidence by comparing it to an ideal rank measured by the original ratings.

`averageRank`

`number`

Determines the goodness of a ranking by computing the percentile rank from the predicted confidence and dividing it by the original rank.

### ArimaForecastingMetrics

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;nonSeasonalOrder&quot;: [{object (ArimaOrder)}],&quot;arimaFittingMetrics&quot;: [{object (ArimaFittingMetrics)}],&quot;seasonalPeriods&quot;: [enum (SeasonalPeriodType)],&quot;hasDrift&quot;: [boolean],&quot;timeSeriesId&quot;: [string],&quot;arimaSingleModelForecastingMetrics&quot;: [{object (ArimaSingleModelForecastingMetrics)}]}</code></pre></td>
</tr>
</tbody>
</table>

Fields

` nonSeasonalOrder[] (deprecated)  `

` object ( ArimaOrder  ` )

> This item is deprecated\!

Non-seasonal order.

` arimaFittingMetrics[] (deprecated)  `

` object ( ArimaFittingMetrics  ` )

> This item is deprecated\!

Arima model fitting metrics.

` seasonalPeriods[] (deprecated)  `

` enum ( SeasonalPeriodType  ` )

> This item is deprecated\!

Seasonal periods. Repeated because multiple periods are supported for one time series.

` hasDrift[] (deprecated)  `

`boolean`

> This item is deprecated\!

Whether Arima model fitted with drift or not. It is always false when d is not 1.

` timeSeriesId[] (deprecated)  `

`string`

> This item is deprecated\!

Id to differentiate different time series for the large-scale case.

`arimaSingleModelForecastingMetrics[]`

` object ( ArimaSingleModelForecastingMetrics  ` )

Repeated as there can be many metric sets (one for each model) in auto-arima and the large-scale case.

### ArimaSingleModelForecastingMetrics

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;nonSeasonalOrder&quot;: {object (ArimaOrder)},&quot;arimaFittingMetrics&quot;: {object (ArimaFittingMetrics)},&quot;hasDrift&quot;: boolean,&quot;timeSeriesId&quot;: string,&quot;timeSeriesIds&quot;: [string],&quot;seasonalPeriods&quot;: [enum (SeasonalPeriodType)],&quot;hasHolidayEffect&quot;: boolean,&quot;hasSpikesAndDips&quot;: boolean,&quot;hasStepChanges&quot;: boolean}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`nonSeasonalOrder`

` object ( ArimaOrder  ` )

Non-seasonal order.

`arimaFittingMetrics`

` object ( ArimaFittingMetrics  ` )

Arima fitting metrics.

`hasDrift`

`boolean`

Is arima model fitted with drift or not. It is always false when d is not 1.

`timeSeriesId`

`string`

The time\_series\_id value for this time series. It will be one of the unique values from the time\_series\_id\_column specified during ARIMA model training. Only present when time\_series\_id\_column training option was used.

`timeSeriesIds[]`

`string`

The tuple of time\_series\_ids identifying this time series. It will be one of the unique tuples of values present in the time\_series\_id\_columns specified during ARIMA model training. Only present when time\_series\_id\_columns training option was used and the order of values here are same as the order of time\_series\_id\_columns.

`seasonalPeriods[]`

` enum ( SeasonalPeriodType  ` )

Seasonal periods. Repeated because multiple periods are supported for one time series.

`hasHolidayEffect`

`boolean`

If true, holiday\_effect is a part of time series decomposition result.

`hasSpikesAndDips`

`boolean`

If true, spikes\_and\_dips is a part of time series decomposition result.

`hasStepChanges`

`boolean`

If true, step\_changes is a part of time series decomposition result.

### DimensionalityReductionMetrics

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;totalExplainedVarianceRatio&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`totalExplainedVarianceRatio`

`number`

Total percentage of variance explained by the selected principal components.

### ExportDataStatistics

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;fileCount&quot;: string,
  &quot;rowCount&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`fileCount`

`string ( Int64Value format)`

Number of destination files generated in case of EXPORT DATA statement only.

`rowCount`

`string ( Int64Value format)`

\[Alpha\] Number of destination rows generated in case of EXPORT DATA statement only.

### ExternalServiceCost

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
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

`externalService`

`string`

External service name.

`bytesProcessed`

`string ( Int64Value format)`

External service cost in terms of bigquery bytes processed.

`bytesBilled`

`string ( Int64Value format)`

External service cost in terms of bigquery bytes billed.

`slotMs`

`string ( Int64Value format)`

External service cost in terms of bigquery slot milliseconds.

`reservedSlotCount`

`string ( int64 format)`

Non-preemptable reserved slots used for external job. For example, reserved slots for Cloua AI Platform job are the VM usages converted to BigQuery slot with equivalent mount of price.

`billingMethod`

`string`

The billing method used for the external job. This field, set to `SERVICES_SKU` , is only used when billing under the services SKU. Otherwise, it is unspecified for backward compatibility.

### BiEngineStatistics

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;biEngineMode&quot;: enum (BiEngineMode),&quot;accelerationMode&quot;: enum (BiEngineAccelerationMode),&quot;biEngineReasons&quot;: [{object (BiEngineReason)}]}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`biEngineMode`

` enum ( BiEngineMode  ` )

Output only. Specifies which mode of BI Engine acceleration was performed (if any).

`accelerationMode`

` enum ( BiEngineAccelerationMode  ` )

Output only. Specifies which mode of BI Engine acceleration was performed (if any).

`biEngineReasons[]`

` object ( BiEngineReason  ` )

In case of DISABLED or PARTIAL bi\_engine\_mode, these contain the explanatory reasons as to why BI Engine could not accelerate. In case the full query was accelerated, this field is not populated.

### BiEngineReason

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;code&quot;: enum (Code),&quot;message&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`code`

` enum ( Code  ` )

Output only. High-level BI Engine reason for partial or disabled acceleration

`message`

`string`

Output only. Free form human-readable reason for partial or disabled acceleration.

### LoadQueryStatistics

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
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

`inputFiles`

`string ( Int64Value format)`

Output only. Number of source files in a LOAD query.

`inputFileBytes`

`string ( Int64Value format)`

Output only. Number of bytes of source data in a LOAD query.

`outputRows`

`string ( Int64Value format)`

Output only. Number of rows imported in a LOAD query. Note that while a LOAD query is in the running state, this value may change.

`outputBytes`

`string ( Int64Value format)`

Output only. Size of the loaded data in bytes. Note that while a LOAD query is in the running state, this value may change.

`badRecords`

`string ( Int64Value format)`

Output only. The number of bad records encountered while processing a LOAD query. Note that if the job has failed because of more bad records encountered than the maximum allowed in the load job configuration, then this number can be less than the total number of bad records present in the input data.

` bytesTransferred (deprecated)  `

`string ( Int64Value format)`

> This item is deprecated\!

Output only. This field is deprecated. The number of bytes of source data copied over the network for a `LOAD` query. `transferred_bytes` has the canonical value for physical transferred bytes, which is used for BigQuery Omni billing.

### SearchStatistics

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;indexUsageMode&quot;: enum (IndexUsageMode),&quot;indexUnusedReasons&quot;: [{object (IndexUnusedReason)}],&quot;indexPruningStats&quot;: [{object (IndexPruningStats)}]}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`indexUsageMode`

` enum ( IndexUsageMode  ` )

Specifies the index usage mode for the query.

`indexUnusedReasons[]`

` object ( IndexUnusedReason  ` )

When `indexUsageMode` is `UNUSED` or `PARTIALLY_USED` , this field explains why indexes were not used in all or part of the search query. If `indexUsageMode` is `FULLY_USED` , this field is not populated.

`indexPruningStats[]`

` object ( IndexPruningStats  ` )

Search index pruning statistics, one for each base table that has a search index. If a base table does not have a search index or the index does not help with pruning on the base table, then there is no pruning statistics for that table.

### IndexUnusedReason

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _code can be only one of the following:&quot;code&quot;: enum (Code)// End of list of possible types for union field _code.// Union field _message can be only one of the following:&quot;message&quot;: string// End of list of possible types for union field _message.// Union field _base_table can be only one of the following:&quot;baseTable&quot;: {object (TableReference)}// End of list of possible types for union field _base_table.// Union field _index_name can be only one of the following:&quot;indexName&quot;: string// End of list of possible types for union field _index_name.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_code` .

`_code` can be only one of the following:

`code`

` enum ( Code  ` )

Specifies the high-level reason for the scenario when no search index was used.

Union field `_message` .

`_message` can be only one of the following:

`message`

`string`

Free form human-readable reason for the scenario when no search index was used.

Union field `_base_table` .

`_base_table` can be only one of the following:

`baseTable`

` object ( TableReference  ` )

Specifies the base table involved in the reason that no search index was used.

Union field `_index_name` .

`_index_name` can be only one of the following:

`indexName`

`string`

Specifies the name of the unused search index, if available.

### IndexPruningStats

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _base_table can be only one of the following:&quot;baseTable&quot;: {object (TableReference)}// End of list of possible types for union field _base_table.// Union field _index_id can be only one of the following:&quot;indexId&quot;: string// End of list of possible types for union field _index_id.// Union field _pre_index_pruning_parallel_input_count can be only one of the// following:&quot;preIndexPruningParallelInputCount&quot;: string// End of list of possible types for union field// _pre_index_pruning_parallel_input_count.// Union field _post_index_pruning_parallel_input_count can be only one of the// following:&quot;postIndexPruningParallelInputCount&quot;: string// End of list of possible types for union field// _post_index_pruning_parallel_input_count.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_base_table` .

`_base_table` can be only one of the following:

`baseTable`

` object ( TableReference  ` )

The base table reference.

Union field `_index_id` .

`_index_id` can be only one of the following:

`indexId`

`string`

The index id.

Union field `_pre_index_pruning_parallel_input_count` .

`_pre_index_pruning_parallel_input_count` can be only one of the following:

`preIndexPruningParallelInputCount`

`string ( int64 format)`

The number of parallel inputs before index pruning.

Union field `_post_index_pruning_parallel_input_count` .

`_post_index_pruning_parallel_input_count` can be only one of the following:

`postIndexPruningParallelInputCount`

`string ( int64 format)`

The number of parallel inputs after index pruning.

### VectorSearchStatistics

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;indexUsageMode&quot;: enum (IndexUsageMode),&quot;indexUnusedReasons&quot;: [{object (IndexUnusedReason)}],&quot;storedColumnsUsages&quot;: [{object (StoredColumnsUsage)}]}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`indexUsageMode`

` enum ( IndexUsageMode  ` )

Specifies the index usage mode for the query.

`indexUnusedReasons[]`

` object ( IndexUnusedReason  ` )

When `indexUsageMode` is `UNUSED` or `PARTIALLY_USED` , this field explains why indexes were not used in all or part of the vector search query. If `indexUsageMode` is `FULLY_USED` , this field is not populated.

`storedColumnsUsages[]`

` object ( StoredColumnsUsage  ` )

Specifies the usage of stored columns in the query when stored columns are used in the query.

### StoredColumnsUsage

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;storedColumnsUnusedReasons&quot;: [{object (StoredColumnsUnusedReason)}],// Union field _is_query_accelerated can be only one of the following:&quot;isQueryAccelerated&quot;: boolean// End of list of possible types for union field _is_query_accelerated.// Union field _base_table can be only one of the following:&quot;baseTable&quot;: {object (TableReference)}// End of list of possible types for union field _base_table.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`storedColumnsUnusedReasons[]`

` object ( StoredColumnsUnusedReason  ` )

If stored columns were not used, explain why.

Union field `_is_query_accelerated` .

`_is_query_accelerated` can be only one of the following:

`isQueryAccelerated`

`boolean`

Specifies whether the query was accelerated with stored columns.

Union field `_base_table` .

`_base_table` can be only one of the following:

`baseTable`

` object ( TableReference  ` )

Specifies the base table.

### StoredColumnsUnusedReason

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;uncoveredColumns&quot;: [string],// Union field _code can be only one of the following:&quot;code&quot;: enum (Code)// End of list of possible types for union field _code.// Union field _message can be only one of the following:&quot;message&quot;: string// End of list of possible types for union field _message.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`uncoveredColumns[]`

`string`

Specifies which columns were not covered by the stored columns for the specified code up to 20 columns. This is populated when the code is STORED\_COLUMNS\_COVER\_INSUFFICIENT and BASE\_TABLE\_HAS\_CLS.

Union field `_code` .

`_code` can be only one of the following:

`code`

` enum ( Code  ` )

Specifies the high-level reason for the unused scenario, each reason must have a code associated.

Union field `_message` .

`_message` can be only one of the following:

`message`

`string`

Specifies the detailed description for the scenario.

### PerformanceInsights

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;avgPreviousExecutionMs&quot;: string,&quot;stagePerformanceStandaloneInsights&quot;: [{object (StagePerformanceStandaloneInsight)}],&quot;stagePerformanceChangeInsights&quot;: [{object (StagePerformanceChangeInsight)}],&quot;tableChangeInsights&quot;: [{object (TableChangeInsight)}]}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`avgPreviousExecutionMs`

`string ( int64 format)`

Output only. Average execution ms of previous runs. Indicates the job ran slow compared to previous executions. To find previous executions, use INFORMATION\_SCHEMA tables and filter jobs with same query hash.

`stagePerformanceStandaloneInsights[]`

` object ( StagePerformanceStandaloneInsight  ` )

Output only. Standalone query stage performance insights, for exploring potential improvements.

`stagePerformanceChangeInsights[]`

` object ( StagePerformanceChangeInsight  ` )

Output only. Query stage performance insights compared to previous runs, for diagnosing performance regression.

`tableChangeInsights[]`

` object ( TableChangeInsight  ` )

Output only. Performance insights for table-level attributes that changed compared to previous runs.

### StagePerformanceStandaloneInsight

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;stageId&quot;: string,&quot;biEngineReasons&quot;: [{object (BiEngineReason)}],&quot;highCardinalityJoins&quot;: [{object (HighCardinalityJoin)}],// Union field _slot_contention can be only one of the following:&quot;slotContention&quot;: boolean// End of list of possible types for union field _slot_contention.// Union field _insufficient_shuffle_quota can be only one of the following:&quot;insufficientShuffleQuota&quot;: boolean// End of list of possible types for union field _insufficient_shuffle_quota.// Union field _partition_skew can be only one of the following:&quot;partitionSkew&quot;: {object (PartitionSkew)}// End of list of possible types for union field _partition_skew.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`stageId`

`string ( int64 format)`

Output only. The stage id that the insight mapped to.

`biEngineReasons[]`

` object ( BiEngineReason  ` )

Output only. If present, the stage had the following reasons for being disqualified from BI Engine execution.

`highCardinalityJoins[]`

` object ( HighCardinalityJoin  ` )

Output only. High cardinality joins in the stage.

Union field `_slot_contention` .

`_slot_contention` can be only one of the following:

`slotContention`

`boolean`

Output only. True if the stage has a slot contention issue.

Union field `_insufficient_shuffle_quota` .

`_insufficient_shuffle_quota` can be only one of the following:

`insufficientShuffleQuota`

`boolean`

Output only. True if the stage has insufficient shuffle quota.

Union field `_partition_skew` .

`_partition_skew` can be only one of the following:

`partitionSkew`

` object ( PartitionSkew  ` )

Output only. Partition skew in the stage.

### HighCardinalityJoin

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;leftRows&quot;: string,
  &quot;rightRows&quot;: string,
  &quot;outputRows&quot;: string,
  &quot;stepIndex&quot;: integer
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`leftRows`

`string ( int64 format)`

Output only. Count of left input rows.

`rightRows`

`string ( int64 format)`

Output only. Count of right input rows.

`outputRows`

`string ( int64 format)`

Output only. Count of the output rows.

`stepIndex`

`integer`

Output only. The index of the join operator in the ExplainQueryStep lists.

### PartitionSkew

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;skewSources&quot;: [{object (SkewSource)}]}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`skewSources[]`

` object ( SkewSource  ` )

Output only. Source stages which produce skewed data.

### SkewSource

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;stageId&quot;: string,
  &quot;outputBytesMedian&quot;: string,
  &quot;outputBytesP95&quot;: string,
  &quot;outputBytesMax&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`stageId`

`string ( int64 format)`

Output only. Stage id of the skew source stage.

`outputBytesMedian`

`string ( int64 format)`

Output only. Median partition output size (in bytes) for this stage.

`outputBytesP95`

`string ( int64 format)`

Output only. 95-th percentile of partition output size (in bytes) for this stage.

`outputBytesMax`

`string ( int64 format)`

Output only. Max partition output size (in bytes) for this stage.

### StagePerformanceChangeInsight

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;stageId&quot;: string,// Union field _input_data_change can be only one of the following:&quot;inputDataChange&quot;: {object (InputDataChange)}// End of list of possible types for union field _input_data_change.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`stageId`

`string ( int64 format)`

Output only. The stage id that the insight mapped to.

Union field `_input_data_change` .

`_input_data_change` can be only one of the following:

`inputDataChange`

` object ( InputDataChange  ` )

Output only. Input data change insight of the query stage.

### InputDataChange

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;recordsReadDiffPercentage&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`recordsReadDiffPercentage`

`number`

Output only. Records read difference percentage compared to a previous run.

### TableChangeInsight

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;tableReference&quot;: {object (TableReference)},// Union field _metadata_cache_staleness_insight can be only one of the// following:&quot;metadataCacheStalenessInsight&quot;: {object (MetadataCacheStalenessInsight)}// End of list of possible types for union field// _metadata_cache_staleness_insight.// Union field _metadata_cache_not_used_but_used_previously can be only one of// the following:&quot;metadataCacheNotUsedButUsedPreviously&quot;: boolean// End of list of possible types for union field// _metadata_cache_not_used_but_used_previously.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`tableReference`

` object ( TableReference  ` )

Output only. The table that was queried.

Union field `_metadata_cache_staleness_insight` .

`_metadata_cache_staleness_insight` can be only one of the following:

`metadataCacheStalenessInsight`

` object ( MetadataCacheStalenessInsight  ` )

Output only. If present, indicates that the table's metadata column index staleness has increased significantly compared to previous jobs with the same query hash.

Union field `_metadata_cache_not_used_but_used_previously` .

`_metadata_cache_not_used_but_used_previously` can be only one of the following:

`metadataCacheNotUsedButUsedPreviously`

`boolean`

Output only. True if the table's column metadata index was not used in the current job, but was used in a previous job with the same query hash.

### MetadataCacheStalenessInsight

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;avgPreviousStalenessMs&quot;: string,
  &quot;stalenessPercentageIncrease&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`avgPreviousStalenessMs`

` string ( Duration  ` format)

Output only. Average column metadata index staleness of previous runs with the same query hash.

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

`stalenessPercentageIncrease`

`number`

Output only. The percent increase in staleness between the current job and the average staleness of previous jobs with the same query hash.

### QueryInfo

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;optimizationDetails&quot;: {
    object
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`optimizationDetails`

` object ( Struct  ` format)

Output only. Information about query optimizations.

### SparkStatistics

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;endpoints&quot;: {string: string,...},// Union field _spark_job_id can be only one of the following:&quot;sparkJobId&quot;: string// End of list of possible types for union field _spark_job_id.// Union field _spark_job_location can be only one of the following:&quot;sparkJobLocation&quot;: string// End of list of possible types for union field _spark_job_location.// Union field _logging_info can be only one of the following:&quot;loggingInfo&quot;: {object (LoggingInfo)}// End of list of possible types for union field _logging_info.// Union field _kms_key_name can be only one of the following:&quot;kmsKeyName&quot;: string// End of list of possible types for union field _kms_key_name.// Union field _gcs_staging_bucket can be only one of the following:&quot;gcsStagingBucket&quot;: string// End of list of possible types for union field _gcs_staging_bucket.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`endpoints`

`map (key: string, value: string)`

Output only. Endpoints returned from Dataproc. Key list: - history\_server\_endpoint: A link to Spark job UI.

An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .

Union field `_spark_job_id` .

`_spark_job_id` can be only one of the following:

`sparkJobId`

`string`

Output only. Spark job ID if a Spark job is created successfully.

Union field `_spark_job_location` .

`_spark_job_location` can be only one of the following:

`sparkJobLocation`

`string`

Output only. Location where the Spark job is executed. A location is selected by BigQueury for jobs configured to run in a multi-region.

Union field `_logging_info` .

`_logging_info` can be only one of the following:

`loggingInfo`

` object ( LoggingInfo  ` )

Output only. Logging info is used to generate a link to Cloud Logging.

Union field `_kms_key_name` .

`_kms_key_name` can be only one of the following:

`kmsKeyName`

`string`

Output only. The Cloud KMS encryption key that is used to protect the resources created by the Spark job. If the Spark procedure uses the invoker security mode, the Cloud KMS encryption key is either inferred from the provided system variable, `@@spark_proc_properties.kms_key_name` , or the default key of the BigQuery job's project (if the CMEK organization policy is enforced). Otherwise, the Cloud KMS key is either inferred from the Spark connection associated with the procedure (if it is provided), or from the default key of the Spark connection's project if the CMEK organization policy is enforced.

Example:

  - `projects/[kms_project_id]/locations/[region]/keyRings/[key_region]/cryptoKeys/[key]`

Union field `_gcs_staging_bucket` .

`_gcs_staging_bucket` can be only one of the following:

`gcsStagingBucket`

`string`

Output only. The Google Cloud Storage bucket that is used as the default file system by the Spark application. This field is only filled when the Spark procedure uses the invoker security mode. The `gcsStagingBucket` bucket is inferred from the `@@spark_proc_properties.staging_bucket` system variable (if it is provided). Otherwise, BigQuery creates a default staging bucket for the job and returns the bucket name in this field.

Example:

  - `gs://[bucket_name]`

### EndpointsEntry

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;key&quot;: string,
  &quot;value&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`key`

`string`

`value`

`string`

### LoggingInfo

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;resourceType&quot;: string,
  &quot;projectId&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`resourceType`

`string`

Output only. Resource type used for logging.

`projectId`

`string`

Output only. Project ID where the Spark logs were written.

### MaterializedViewStatistics

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;materializedView&quot;: [{object (MaterializedView)}]}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`materializedView[]`

` object ( MaterializedView  ` )

Materialized views considered for the query job. Only certain materialized views are used. For a detailed list, see the child message.

If many materialized views are considered, then the list might be incomplete.

### MaterializedView

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _table_reference can be only one of the following:&quot;tableReference&quot;: {object (TableReference)}// End of list of possible types for union field _table_reference.// Union field _chosen can be only one of the following:&quot;chosen&quot;: boolean// End of list of possible types for union field _chosen.// Union field _estimated_bytes_saved can be only one of the following:&quot;estimatedBytesSaved&quot;: string// End of list of possible types for union field _estimated_bytes_saved.// Union field _rejected_reason can be only one of the following:&quot;rejectedReason&quot;: enum (RejectedReason)// End of list of possible types for union field _rejected_reason.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_table_reference` .

`_table_reference` can be only one of the following:

`tableReference`

` object ( TableReference  ` )

The candidate materialized view.

Union field `_chosen` .

`_chosen` can be only one of the following:

`chosen`

`boolean`

Whether the materialized view is chosen for the query.

A materialized view can be chosen to rewrite multiple parts of the same query. If a materialized view is chosen to rewrite any part of the query, then this field is true, even if the materialized view was not chosen to rewrite others parts.

Union field `_estimated_bytes_saved` .

`_estimated_bytes_saved` can be only one of the following:

`estimatedBytesSaved`

`string ( int64 format)`

If present, specifies a best-effort estimation of the bytes saved by using the materialized view rather than its base tables.

Union field `_rejected_reason` .

`_rejected_reason` can be only one of the following:

`rejectedReason`

` enum ( RejectedReason  ` )

If present, specifies the reason why the materialized view was not chosen for the query.

### MetadataCacheStatistics

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;tableMetadataCacheUsage&quot;: [{object (TableMetadataCacheUsage)}]}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`tableMetadataCacheUsage[]`

` object ( TableMetadataCacheUsage  ` )

Set for the Metadata caching eligible tables referenced in the query.

### TableMetadataCacheUsage

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;staleness&quot;: string,&quot;tableType&quot;: string,// Union field _table_reference can be only one of the following:&quot;tableReference&quot;: {object (TableReference)}// End of list of possible types for union field _table_reference.// Union field _unused_reason can be only one of the following:&quot;unusedReason&quot;: enum (UnusedReason)// End of list of possible types for union field _unused_reason.// Union field _explanation can be only one of the following:&quot;explanation&quot;: string// End of list of possible types for union field _explanation.// Union field _pruning_stats can be only one of the following:&quot;pruningStats&quot;: {object (PruningStats)}// End of list of possible types for union field _pruning_stats.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`staleness`

` string ( Duration  ` format)

Duration since last refresh as of this job for managed tables (indicates metadata cache staleness as seen by this job).

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

`tableType`

`string`

[Table type](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#Table.FIELDS.type) .

Union field `_table_reference` .

`_table_reference` can be only one of the following:

`tableReference`

` object ( TableReference  ` )

Metadata caching eligible table referenced in the query.

Union field `_unused_reason` .

`_unused_reason` can be only one of the following:

`unusedReason`

` enum ( UnusedReason  ` )

Reason for not using metadata caching for the table.

Union field `_explanation` .

`_explanation` can be only one of the following:

`explanation`

`string`

Free form human-readable reason metadata caching was unused for the job.

Union field `_pruning_stats` .

`_pruning_stats` can be only one of the following:

`pruningStats`

` object ( PruningStats  ` )

The column metadata index pruning statistics.

### PruningStats

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _post_cmeta_pruning_partition_count can be only one of the// following:&quot;postCmetaPruningPartitionCount&quot;: string// End of list of possible types for union field// _post_cmeta_pruning_partition_count.// Union field _pre_cmeta_pruning_parallel_input_count can be only one of the// following:&quot;preCmetaPruningParallelInputCount&quot;: string// End of list of possible types for union field// _pre_cmeta_pruning_parallel_input_count.// Union field _post_cmeta_pruning_parallel_input_count can be only one of the// following:&quot;postCmetaPruningParallelInputCount&quot;: string// End of list of possible types for union field// _post_cmeta_pruning_parallel_input_count.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_post_cmeta_pruning_partition_count` .

`_post_cmeta_pruning_partition_count` can be only one of the following:

`postCmetaPruningPartitionCount`

`string ( int64 format)`

The number of partitions matched.

Union field `_pre_cmeta_pruning_parallel_input_count` .

`_pre_cmeta_pruning_parallel_input_count` can be only one of the following:

`preCmetaPruningParallelInputCount`

`string ( int64 format)`

The number of parallel inputs scanned.

Union field `_post_cmeta_pruning_parallel_input_count` .

`_post_cmeta_pruning_parallel_input_count` can be only one of the following:

`postCmetaPruningParallelInputCount`

`string ( int64 format)`

The number of parallel inputs matched.

### IncrementalResultStats

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;disabledReason&quot;: enum (DisabledReason),&quot;disabledReasonDetails&quot;: string,&quot;resultSetLastReplaceTime&quot;: string,&quot;resultSetLastModifyTime&quot;: string,&quot;firstIncrementalRowTime&quot;: string,&quot;lastIncrementalRowTime&quot;: string,// Union field _incremental_row_count can be only one of the following:&quot;incrementalRowCount&quot;: string// End of list of possible types for union field _incremental_row_count.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`disabledReason`

` enum ( DisabledReason  ` )

Output only. Reason why incremental query results are/were not written by the query.

`disabledReasonDetails`

`string`

Output only. Additional human-readable clarification, if available, for DisabledReason.

`resultSetLastReplaceTime`

` string ( Timestamp  ` format)

Output only. The time at which the result table's contents were completely replaced. May be absent if no results have been written or the query has completed.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`resultSetLastModifyTime`

` string ( Timestamp  ` format)

Output only. The time at which the result table's contents were modified. May be absent if no results have been written or the query has completed.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`firstIncrementalRowTime`

` string ( Timestamp  ` format)

Output only. The time at which the first incremental result was written. If the query needed to restart internally, this only describes the final attempt.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`lastIncrementalRowTime`

` string ( Timestamp  ` format)

Output only. The time at which the last incremental result was written. Does not include the final result written after query completion.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

Union field `_incremental_row_count` .

`_incremental_row_count` can be only one of the following:

`incrementalRowCount`

`string ( int64 format)`

Output only. Number of rows that were in the latest result set before query completion.

### GenAiStats

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;functionStats&quot;: [{object (GenAiFunctionStats)}],// Union field _error_stats can be only one of the following:&quot;errorStats&quot;: {object (GenAiErrorStats)}// End of list of possible types for union field _error_stats.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`functionStats[]`

` object ( GenAiFunctionStats  ` )

Function level stats for GenAI Functions. For more information, see [Generative AI overview](https://docs.cloud.google.com/bigquery/docs/generative-ai-overview) .

Union field `_error_stats` .

`_error_stats` can be only one of the following:

`errorStats`

` object ( GenAiErrorStats  ` )

Job level error stats across all GenAi functions

### GenAiErrorStats

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;errors&quot;: [
    string
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`errors[]`

`string`

A list of unique errors at query level (up to 5, truncated to 100 chars)

### GenAiFunctionStats

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _function_name can be only one of the following:&quot;functionName&quot;: string// End of list of possible types for union field _function_name.// Union field _prompt can be only one of the following:&quot;prompt&quot;: string// End of list of possible types for union field _prompt.// Union field _num_processed_rows can be only one of the following:&quot;numProcessedRows&quot;: string// End of list of possible types for union field _num_processed_rows.// Union field _error_stats can be only one of the following:&quot;errorStats&quot;: {object (GenAiFunctionErrorStats)}// End of list of possible types for union field _error_stats.// Union field _cost_optimization_stats can be only one of the following:&quot;costOptimizationStats&quot;: {object (GenAiFunctionCostOptimizationStats)}// End of list of possible types for union field _cost_optimization_stats.// Union field _cache_stats can be only one of the following:&quot;cacheStats&quot;: {object (GenAiFunctionCacheStats)}// End of list of possible types for union field _cache_stats.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_function_name` .

`_function_name` can be only one of the following:

`functionName`

`string`

Name of the function.

Union field `_prompt` .

`_prompt` can be only one of the following:

`prompt`

`string`

User input prompt of the function (truncated to 20 chars).

Union field `_num_processed_rows` .

`_num_processed_rows` can be only one of the following:

`numProcessedRows`

`string ( int64 format)`

Number of rows processed by this GenAi function. This includes all cost\_optimized, llm\_inferred and failed\_rows.

Union field `_error_stats` .

`_error_stats` can be only one of the following:

`errorStats`

` object ( GenAiFunctionErrorStats  ` )

Error stats for the function.

Union field `_cost_optimization_stats` .

`_cost_optimization_stats` can be only one of the following:

`costOptimizationStats`

` object ( GenAiFunctionCostOptimizationStats  ` )

Cost optimization stats if applied on the rows processed by the function.

Union field `_cache_stats` .

`_cache_stats` can be only one of the following:

`cacheStats`

` object ( GenAiFunctionCacheStats  ` )

Cache stats for the function.

### GenAiFunctionErrorStats

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;errors&quot;: [
    string
  ],
  &quot;numFailedRows&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`errors[]`

`string`

A list of unique errors at function level (up to 5, truncated to 100 chars).

`numFailedRows`

`string ( int64 format)`

Number of failed rows processed by the function

### GenAiFunctionCostOptimizationStats

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _num_cost_optimized_rows can be only one of the following:&quot;numCostOptimizedRows&quot;: string// End of list of possible types for union field _num_cost_optimized_rows.// Union field _message can be only one of the following:&quot;message&quot;: string// End of list of possible types for union field _message.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_num_cost_optimized_rows` .

`_num_cost_optimized_rows` can be only one of the following:

`numCostOptimizedRows`

`string ( int64 format)`

Number of rows inferred via cost optimized workflow.

Union field `_message` .

`_message` can be only one of the following:

`message`

`string`

System generated message to provide insights into cost optimization state.

### GenAiFunctionCacheStats

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _num_cache_hit_rows can be only one of the following:&quot;numCacheHitRows&quot;: string// End of list of possible types for union field _num_cache_hit_rows.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_num_cache_hit_rows` .

`_num_cache_hit_rows` can be only one of the following:

`numCacheHitRows`

`string ( int64 format)`

Number of rows served from cache.

### ObjectStorageStats

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _cloud_provider can be only one of the following:&quot;cloudProvider&quot;: enum (CloudProvider)// End of list of possible types for union field _cloud_provider.// Union field _object_storage_bytes_read can be only one of the following:&quot;objectStorageBytesRead&quot;: string// End of list of possible types for union field _object_storage_bytes_read.// Union field _cache_bytes_read can be only one of the following:&quot;cacheBytesRead&quot;: string// End of list of possible types for union field _cache_bytes_read.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_cloud_provider` .

`_cloud_provider` can be only one of the following:

`cloudProvider`

` enum ( CloudProvider  ` )

The cloud provider for this block of statistics.

Union field `_object_storage_bytes_read` .

`_object_storage_bytes_read` can be only one of the following:

`objectStorageBytesRead`

`string ( int64 format)`

Total bytes read directly from the cloud provider's storage.

Union field `_cache_bytes_read` .

`_cache_bytes_read` can be only one of the following:

`cacheBytesRead`

`string ( int64 format)`

Total bytes read from the GCP Lakehouse-internal cache, avoiding an object storage read.

### JobStatistics3

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;inputFiles&quot;: string,&quot;inputFileBytes&quot;: string,&quot;outputRows&quot;: string,&quot;outputBytes&quot;: string,&quot;badRecords&quot;: string,&quot;timeline&quot;: [{object (QueryTimelineSample)}]}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`inputFiles`

`string ( Int64Value format)`

Output only. Number of source files in a load job.

`inputFileBytes`

`string ( Int64Value format)`

Output only. Number of bytes of source data in a load job.

`outputRows`

`string ( Int64Value format)`

Output only. Number of rows imported in a load job. Note that while an import job is in the running state, this value may change.

`outputBytes`

`string ( Int64Value format)`

Output only. Size of the loaded data in bytes. Note that while a load job is in the running state, this value may change.

`badRecords`

`string ( Int64Value format)`

Output only. The number of bad records encountered. Note that if the job has failed because of more bad records encountered than the maximum allowed in the load job configuration, then this number can be less than the total number of bad records present in the input data.

`timeline[]`

` object ( QueryTimelineSample  ` )

Output only. Describes a timeline of job execution.

### JobStatistics4

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;destinationUriFileCounts&quot;: [string],&quot;inputBytes&quot;: string,&quot;timeline&quot;: [{object (QueryTimelineSample)}]}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`destinationUriFileCounts[]`

`string ( int64 format)`

Output only. Number of files per destination URI or URI pattern specified in the extract configuration. These values will be in the same order as the URIs specified in the 'destinationUris' field.

`inputBytes`

`string ( Int64Value format)`

Output only. Number of user bytes extracted into the result. This is the byte count as computed by BigQuery for billing purposes and doesn't have any relationship with the number of actual result bytes extracted in the desired format.

`timeline[]`

` object ( QueryTimelineSample  ` )

Output only. Describes a timeline of job execution.

### CopyJobStatistics

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;copiedRows&quot;: string,
  &quot;copiedLogicalBytes&quot;: string,
  &quot;remoteDestinationRegion&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`copiedRows`

`string ( Int64Value format)`

Output only. Number of rows copied to the destination table.

`copiedLogicalBytes`

`string ( Int64Value format)`

Output only. Number of logical bytes copied to the destination table.

`remoteDestinationRegion`

`string`

Output only. Destination region for a cross-region copy job. Not set for in-region copy jobs.

### ScriptStatistics

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;evaluationKind&quot;: enum (EvaluationKind),&quot;stackFrames&quot;: [{object (ScriptStackFrame)}]}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`evaluationKind`

` enum ( EvaluationKind  ` )

Whether this child job was a statement or expression.

`stackFrames[]`

` object ( ScriptStackFrame  ` )

Stack trace showing the line/column/procedure name of each frame on the stack at the point where the current evaluation happened. The leaf frame is first, the primary script is last. Never empty.

### ScriptStackFrame

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
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

`startLine`

`integer`

Output only. One-based start line.

`startColumn`

`integer`

Output only. One-based start column.

`endLine`

`integer`

Output only. One-based end line.

`endColumn`

`integer`

Output only. One-based end column.

`procedureId`

`string`

Output only. Name of the active procedure, empty if in a top-level script.

`text`

`string`

Output only. Text of the current statement/expression.

### RowLevelSecurityStatistics

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;rowLevelSecurityApplied&quot;: boolean
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`rowLevelSecurityApplied`

`boolean`

Whether any accessed data was protected by row access policies.

### DataMaskingStatistics

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;dataMaskingApplied&quot;: boolean
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`dataMaskingApplied`

`boolean`

Whether any accessed data was protected by the data masking.

### TransactionInfo

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;transactionId&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`transactionId`

`string`

Output only. \[Alpha\] Id of the transaction.

### SessionInfo

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;sessionId&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`sessionId`

`string`

Output only. The id of the session.

### JobStatus

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;errorResult&quot;: {object (ErrorProto)},&quot;errors&quot;: [{object (ErrorProto)}],&quot;state&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`errorResult`

` object ( ErrorProto  ` )

Output only. Final error result of the job. If present, indicates that the job has completed and was unsuccessful.

`errors[]`

` object ( ErrorProto  ` )

Output only. The first errors encountered during the running of the job. The final message includes the number of errors that caused the process to stop. Errors here do not necessarily mean that the job has not completed or was unsuccessful.

`state`

`string`

Output only. Running state of the job. Valid states include 'PENDING', 'RUNNING', and 'DONE'.

### ErrorProto

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;reason&quot;: string,
  &quot;location&quot;: string,
  &quot;debugInfo&quot;: string,
  &quot;message&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`reason`

`string`

A short error code that summarizes the error.

`location`

`string`

Specifies where the error occurred, if present.

`debugInfo`

`string`

Debugging information. This property is internal to Google and should not be used.

`message`

`string`

A human-readable description of the error.

### JobCreationReason

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;code&quot;: enum (Code)}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`code`

` enum ( Code  ` )

Output only. Specifies the high level reason why a Job was created.

### FileSetSpecType

This enum defines how to interpret source URIs for load jobs and external tables.

Enums

`FILE_SET_SPEC_TYPE_FILE_SYSTEM_MATCH`

This option expands source URIs by listing files from the object store. It is the default behavior if FileSetSpecType is not set.

`FILE_SET_SPEC_TYPE_NEW_LINE_DELIMITED_MANIFEST`

This option indicates that the provided URIs are newline-delimited manifest files, with one URI per line. Wildcard URIs are not supported.

### RoundingMode

Rounding mode options that can be used when storing NUMERIC or BIGNUMERIC values.

Enums

`ROUNDING_MODE_UNSPECIFIED`

Unspecified will default to using ROUND\_HALF\_AWAY\_FROM\_ZERO.

`ROUND_HALF_AWAY_FROM_ZERO`

ROUND\_HALF\_AWAY\_FROM\_ZERO rounds half values away from zero when applying precision and scale upon writing of NUMERIC and BIGNUMERIC values. For Scale: 0 1.1, 1.2, 1.3, 1.4 =\> 1 1.5, 1.6, 1.7, 1.8, 1.9 =\> 2

`ROUND_HALF_EVEN`

ROUND\_HALF\_EVEN rounds half values to the nearest even value when applying precision and scale upon writing of NUMERIC and BIGNUMERIC values. For Scale: 0 1.1, 1.2, 1.3, 1.4 =\> 1 1.5 =\> 2 1.6, 1.7, 1.8, 1.9 =\> 2 2.5 =\> 2

### GeneratedMode

Dictates when system generated values are used to populate the field.

Enums

`GENERATED_MODE_UNSPECIFIED`

Unspecified GeneratedMode will default to GENERATED\_ALWAYS.

`GENERATED_ALWAYS`

Field can only have system generated values. Users cannot manually insert values into the field.

`GENERATED_BY_DEFAULT`

Use system generated values only if the user does not explicitly provide a value.

### TypeSystem

External systems, such as query engines or table formats, that have their own data types.

Enums

`TYPE_SYSTEM_UNSPECIFIED`

TypeSystem not specified.

`HIVE`

Represents Hive data types.

### DecimalTargetType

The data types that could be used as a target type when converting decimal values.

Enums

`DECIMAL_TARGET_TYPE_UNSPECIFIED`

Invalid type.

`NUMERIC`

Decimal values could be converted to NUMERIC type.

`BIGNUMERIC`

Decimal values could be converted to BIGNUMERIC type.

`STRING`

Decimal values could be converted to STRING type.

### JsonExtension

Used to indicate that a JSON variant, rather than normal JSON, is being used as the source\_format. This should only be used in combination with the JSON source format.

Enums

`JSON_EXTENSION_UNSPECIFIED`

The default if provided value is not one included in the enum, or the value is not specified. The source format is parsed without any modification.

`GEOJSON`

Use GeoJSON variant of JSON. See <https://tools.ietf.org/html/rfc7946> .

### MapTargetType

Indicates the map target type. Only applies to parquet maps.

Enums

`MAP_TARGET_TYPE_UNSPECIFIED`

In this mode, the map will have the following schema: struct map\_field\_name { repeated struct key\_value { key value } }.

`ARRAY_OF_STRUCT`

In this mode, the map will have the following schema: repeated struct map\_field\_name { key value }.

### ObjectMetadata

Supported Object Metadata Types.

Enums

`OBJECT_METADATA_UNSPECIFIED`

Unspecified by default.

`DIRECTORY`

A synonym for `SIMPLE` .

`SIMPLE`

Directory listing of objects.

### MetadataCacheMode

MetadataCacheMode identifies if the table should use metadata caching for files from external source (eg Google Cloud Storage).

Enums

`METADATA_CACHE_MODE_UNSPECIFIED`

Unspecified metadata cache mode.

`AUTOMATIC`

Set this mode to trigger automatic background refresh of metadata cache from the external source. Queries will use the latest available cache version within the table's maxStaleness interval.

`MANUAL`

Set this mode to enable triggering manual refresh of the metadata cache from external source. Queries will use the latest manually triggered cache version within the table's maxStaleness interval.

### TypeKind

The kind of the datatype.

Enums

`TYPE_KIND_UNSPECIFIED`

Invalid type.

`INT64`

Encoded as a string in decimal format.

`BOOL`

Encoded as a boolean "false" or "true".

`FLOAT64`

Encoded as a number, or string "NaN", "Infinity" or "-Infinity".

`STRING`

Encoded as a string value.

`BYTES`

Encoded as a base64 string per RFC 4648, section 4.

`TIMESTAMP`

Encoded as an RFC 3339 timestamp with mandatory "Z" time zone string: 1985-04-12T23:20:50.52Z

`DATE`

Encoded as RFC 3339 full-date format string: 1985-04-12

`TIME`

Encoded as RFC 3339 partial-time format string: 23:20:50.52

`DATETIME`

Encoded as RFC 3339 full-date "T" partial-time: 1985-04-12T23:20:50.52

`INTERVAL`

Encoded as fully qualified 3 part: 0-5 15 2:30:45.6

`GEOGRAPHY`

Encoded as WKT

`NUMERIC`

Encoded as a decimal string.

`BIGNUMERIC`

Encoded as a decimal string.

`JSON`

Encoded as a string.

`ARRAY`

Encoded as a list with types matching Type.array\_type.

`STRUCT`

Encoded as a list with fields of type Type.struct\_type\[i\]. List is used because a JSON object cannot have duplicate field names.

`RANGE`

Encoded as a pair with types matching range\_element\_type. Pairs must begin with "\[", end with ")", and be separated by ", ".

`UUID`

Encoded as a string.

### NullValue

Represents a JSON `null` .

`NullValue` is a sentinel, using an enum with only one value to represent the null value for the `Value` type union.

A field of type `NullValue` with any value other than `0` is considered invalid. Most ProtoJSON serializers will emit a `Value` with a `null_value` set as a JSON `null` regardless of the integer value, and so will round trip to a `0` value.

Enums

`NULL_VALUE`

Null value.

### KeyResultStatementKind

KeyResultStatementKind controls how the key result is determined.

Enums

`KEY_RESULT_STATEMENT_KIND_UNSPECIFIED`

Default value.

`LAST`

The last result determines the key result.

`FIRST_SELECT`

The first SELECT statement determines the key result.

### DeserializationOption

`DeserializationOption` defines the `TProtocol` implementation that will be used to deserialize Thrift data.

Enums

`DESERIALIZATION_OPTION_UNSPECIFIED`

Default value. This value is unused.

`THRIFT_BINARY_PROTOCOL_OPTION`

Use `TBinaryProtocol` to deserialize the data..

### FramingOption

Framing in Apache Thrift means 4 bytes added in front of the serialized record or data blocks to inidicate the size of the followed record or data block. Please see `TFramedTransport` for more details. One thing to note is that the 4-byte record size added by `TFramedTransport` is in big endian. A `TFramedTransport` framed block looks like:

| 4-byte size (big endian) | serialized record ... |

We also support framing with little endian record or data block size.

Enums

`FRAMING_OPTION_UNSPECIFIED`

Default value. This value is unused.

`NOT_FRAMED`

Records or data blocks are not framed.

`FRAMED_WITH_BIG_ENDIAN`

Records or data blocks are framed with a 4-byte record size in big endian.

`FRAMED_WITH_LITTLE_ENDIAN`

Records or data blocks are framed with a 4-byte record size in little endian.

### ColumnNameCharacterMap

Indicates the character map used for column names.

Enums

`COLUMN_NAME_CHARACTER_MAP_UNSPECIFIED`

Unspecified column name character map.

`STRICT`

Support flexible column name and reject invalid column names.

`V1`

Support alphanumeric + underscore characters and names must start with a letter or underscore. Invalid column names will be normalized.

`V2`

Support flexible column name. Invalid column names will be normalized.

### SourceColumnMatch

Indicates the strategy used to match loaded columns to the schema.

Enums

`SOURCE_COLUMN_MATCH_UNSPECIFIED`

Uses sensible defaults based on how the schema is provided. If autodetect is used, then columns are matched by name. Otherwise, columns are matched by position. This is done to keep the behavior backward-compatible.

`POSITION`

Matches by position. This assumes that the columns are ordered the same way as the schema.

`NAME`

Matches by name. This reads the header row as column names and reorders columns to match the field names in the schema.

### OperationType

Indicates different operation types supported in table copy job.

Enums

`OPERATION_TYPE_UNSPECIFIED`

Unspecified operation type.

`COPY`

The source and destination table have the same table type.

`SNAPSHOT`

The source table type is TABLE and the destination table type is SNAPSHOT.

`RESTORE`

The source table type is SNAPSHOT and the destination table type is TABLE.

`CLONE`

The source and destination table have the same table type, but only bill for unique data.

### ComputeMode

Indicates the type of compute mode.

Enums

`COMPUTE_MODE_UNSPECIFIED`

ComputeMode type not specified.

`BIGQUERY`

This stage was processed using BigQuery slots.

`BI_ENGINE`

This stage was processed using BI Engine compute.

### DmlMode

Enum to specify the DML mode used.

Enums

`DML_MODE_UNSPECIFIED`

Default value. This value is unused.

`COARSE_GRAINED_DML`

Coarse-grained DML was used.

`FINE_GRAINED_DML`

Fine-grained DML was used.

### FineGrainedDmlUnusedReason

Reason for disabling fine-grained DML. Additional values may be added in the future.

Enums

`FINE_GRAINED_DML_UNUSED_REASON_UNSPECIFIED`

Default value. This value is unused.

`MAX_PARTITION_SIZE_EXCEEDED`

Max partition size threshold exceeded. [Fine-grained DML Limitations](https://docs.cloud.google.com/bigquery/docs/data-manipulation-language#fine-grained-dml-limitations)

`TABLE_NOT_ENROLLED`

The table is not enrolled for fine-grained DML.

`DML_IN_MULTI_STATEMENT_TRANSACTION`

The DML statement is part of a multi-statement transaction.

### SeasonalPeriodType

Seasonal period type.

Enums

`SEASONAL_PERIOD_TYPE_UNSPECIFIED`

Unspecified seasonal period.

`NO_SEASONALITY`

No seasonality

`DAILY`

Daily period, 24 hours.

`WEEKLY`

Weekly period, 7 days.

`MONTHLY`

Monthly period, 30 days or irregular.

`QUARTERLY`

Quarterly period, 90 days or irregular.

`YEARLY`

Yearly period, 365 days or irregular.

`HOURLY`

Hourly period, 1 hour.

### ModelType

Indicates the type of the Model.

Enums

`MODEL_TYPE_UNSPECIFIED`

Default value.

`LINEAR_REGRESSION`

Linear regression model.

`LOGISTIC_REGRESSION`

Logistic regression based classification model.

`KMEANS`

K-means clustering model.

`MATRIX_FACTORIZATION`

Matrix factorization model.

`DNN_CLASSIFIER`

DNN classifier model.

`TENSORFLOW`

An imported TensorFlow model.

`DNN_REGRESSOR`

DNN regressor model.

`XGBOOST`

An imported XGBoost model.

`BOOSTED_TREE_REGRESSOR`

Boosted tree regressor model.

`BOOSTED_TREE_CLASSIFIER`

Boosted tree classifier model.

`ARIMA`

ARIMA model.

`AUTOML_REGRESSOR`

AutoML Tables regression model.

`AUTOML_CLASSIFIER`

AutoML Tables classification model.

`PCA`

Prinpical Component Analysis model.

`DNN_LINEAR_COMBINED_CLASSIFIER`

Wide-and-deep classifier model.

`DNN_LINEAR_COMBINED_REGRESSOR`

Wide-and-deep regressor model.

`AUTOENCODER`

Autoencoder model.

`ARIMA_PLUS`

New name for the ARIMA model.

`ARIMA_PLUS_XREG`

ARIMA with external regressors.

`RANDOM_FOREST_REGRESSOR`

Random forest regressor model.

`RANDOM_FOREST_CLASSIFIER`

Random forest classifier model.

`TENSORFLOW_LITE`

An imported TensorFlow Lite model.

`ONNX`

An imported ONNX model.

`TRANSFORM_ONLY`

Model to capture the columns and logic in the TRANSFORM clause along with statistics useful for ML analytic functions.

`CONTRIBUTION_ANALYSIS`

The contribution analysis model.

### TrainingType

Training type.

Enums

`TRAINING_TYPE_UNSPECIFIED`

Unspecified training type.

`SINGLE_TRAINING`

Single training with fixed parameter space.

`HPARAM_TUNING`

[Hyperparameter tuning training](https://cloud.google.com/bigquery-ml/docs/reference/standard-sql/bigqueryml-syntax-hp-tuning-overview) .

### LossType

Loss metric to evaluate model training performance.

Enums

`LOSS_TYPE_UNSPECIFIED`

Default value.

`MEAN_SQUARED_LOSS`

Mean squared loss, used for linear regression.

`MEAN_LOG_LOSS`

Mean log loss, used for logistic regression.

### DataSplitMethod

Indicates the method to split input data into multiple tables.

Enums

`DATA_SPLIT_METHOD_UNSPECIFIED`

Default value.

`RANDOM`

Splits data randomly.

`CUSTOM`

Splits data with the user provided tags.

`SEQUENTIAL`

Splits data sequentially.

`NO_SPLIT`

Data split will be skipped.

`AUTO_SPLIT`

Splits data automatically: Uses NO\_SPLIT if the data size is small. Otherwise uses RANDOM.

### LearnRateStrategy

Indicates the learning rate optimization strategy to use.

Enums

`LEARN_RATE_STRATEGY_UNSPECIFIED`

Default value.

`LINE_SEARCH`

Use line search to determine learning rate.

`CONSTANT`

Use a constant learning rate.

### DistanceType

Distance metric used to compute the distance between two points.

Enums

`DISTANCE_TYPE_UNSPECIFIED`

Default value.

`EUCLIDEAN`

Eculidean distance.

`COSINE`

Cosine distance.

### OptimizationStrategy

Indicates the optimization strategy used for training.

Enums

`OPTIMIZATION_STRATEGY_UNSPECIFIED`

Default value.

`BATCH_GRADIENT_DESCENT`

Uses an iterative batch gradient descent algorithm.

`NORMAL_EQUATION`

Uses a normal equation to solve linear regression problem.

### BoosterType

Booster types supported. Refer to booster parameter in XGBoost.

Enums

`BOOSTER_TYPE_UNSPECIFIED`

Unspecified booster type.

`GBTREE`

Gbtree booster.

`DART`

Dart booster.

### DartNormalizeType

Type of normalization algorithm for boosted tree models using dart booster. Refer to normalize\_type in XGBoost.

Enums

`DART_NORMALIZE_TYPE_UNSPECIFIED`

Unspecified dart normalize type.

`TREE`

New trees have the same weight of each of dropped trees.

`FOREST`

New trees have the same weight of sum of dropped trees.

### TreeMethod

Tree construction algorithm used in boosted tree models. Refer to tree\_method in XGBoost.

Enums

`TREE_METHOD_UNSPECIFIED`

Unspecified tree method.

`AUTO`

Use heuristic to choose the fastest method.

`EXACT`

Exact greedy algorithm.

`APPROX`

Approximate greedy algorithm using quantile sketch and gradient histogram.

`HIST`

Fast histogram optimized approximate greedy algorithm.

### FeedbackType

Indicates the training algorithm to use for matrix factorization models.

Enums

`FEEDBACK_TYPE_UNSPECIFIED`

Default value.

`IMPLICIT`

Use weighted-als for implicit feedback problems.

`EXPLICIT`

Use nonweighted-als for explicit feedback problems.

### KmeansInitializationMethod

Indicates the method used to initialize the centroids for KMeans clustering algorithm.

Enums

`KMEANS_INITIALIZATION_METHOD_UNSPECIFIED`

Unspecified initialization method.

`RANDOM`

Initializes the centroids randomly.

`CUSTOM`

Initializes the centroids using data specified in kmeans\_initialization\_column.

`KMEANS_PLUS_PLUS`

Initializes with kmeans++.

### DataFrequency

Type of supported data frequency for time series forecasting models.

Enums

`DATA_FREQUENCY_UNSPECIFIED`

Default value.

`AUTO_FREQUENCY`

Automatically inferred from timestamps.

`YEARLY`

Yearly data.

`QUARTERLY`

Quarterly data.

`MONTHLY`

Monthly data.

`WEEKLY`

Weekly data.

`DAILY`

Daily data.

`HOURLY`

Hourly data.

`PER_MINUTE`

Per-minute data.

### HolidayRegion

Type of supported holiday regions for time series forecasting models.

Enums

`HOLIDAY_REGION_UNSPECIFIED`

Holiday region unspecified.

`GLOBAL`

Global.

`NA`

North America.

`JAPAC`

Japan and Asia Pacific: Korea, Greater China, India, Australia, and New Zealand.

`EMEA`

Europe, the Middle East and Africa.

`LAC`

Latin America and the Caribbean.

`AE`

United Arab Emirates

`AR`

Argentina

`AT`

Austria

`AU`

Australia

`BE`

Belgium

`BR`

Brazil

`CA`

Canada

`CH`

Switzerland

`CL`

Chile

`CN`

China

`CO`

Colombia

`CS`

Czechoslovakia

`CZ`

Czech Republic

`DE`

Germany

`DK`

Denmark

`DZ`

Algeria

`EC`

Ecuador

`EE`

Estonia

`EG`

Egypt

`ES`

Spain

`FI`

Finland

`FR`

France

`GB`

Great Britain (United Kingdom)

`GR`

Greece

`HK`

Hong Kong

`HU`

Hungary

`ID`

Indonesia

`IE`

Ireland

`IL`

Israel

`IN`

India

`IR`

Iran

`IT`

Italy

`JP`

Japan

`KR`

Korea (South)

`LV`

Latvia

`MA`

Morocco

`MX`

Mexico

`MY`

Malaysia

`NG`

Nigeria

`NL`

Netherlands

`NO`

Norway

`NZ`

New Zealand

`PE`

Peru

`PH`

Philippines

`PK`

Pakistan

`PL`

Poland

`PT`

Portugal

`RO`

Romania

`RS`

Serbia

`RU`

Russian Federation

`SA`

Saudi Arabia

`SE`

Sweden

`SG`

Singapore

`SI`

Slovenia

`SK`

Slovakia

`TH`

Thailand

`TR`

Turkey

`TW`

Taiwan

`UA`

Ukraine

`US`

United States

`VE`

Venezuela

`VN`

Vietnam

`ZA`

South Africa

### HparamTuningObjective

Available evaluation metrics used as hyperparameter tuning objectives.

Enums

`HPARAM_TUNING_OBJECTIVE_UNSPECIFIED`

Unspecified evaluation metric.

`MEAN_ABSOLUTE_ERROR`

Mean absolute error. mean\_absolute\_error = AVG(ABS(label - predicted))

`MEAN_SQUARED_ERROR`

Mean squared error. mean\_squared\_error = AVG(POW(label - predicted, 2))

`MEAN_SQUARED_LOG_ERROR`

Mean squared log error. mean\_squared\_log\_error = AVG(POW(LN(1 + label) - LN(1 + predicted), 2))

`MEDIAN_ABSOLUTE_ERROR`

Mean absolute error. median\_absolute\_error = APPROX\_QUANTILES(absolute\_error, 2)\[OFFSET(1)\]

`R_SQUARED`

R^2 score. This corresponds to r2\_score in ML.EVALUATE. r\_squared = 1 - SUM(squared\_error)/(COUNT(label)\*VAR\_POP(label))

`EXPLAINED_VARIANCE`

Explained variance. explained\_variance = 1 - VAR\_POP(label\_error)/VAR\_POP(label)

`PRECISION`

Precision is the fraction of actual positive predictions that had positive actual labels. For multiclass this is a macro-averaged metric treating each class as a binary classifier.

`RECALL`

Recall is the fraction of actual positive labels that were given a positive prediction. For multiclass this is a macro-averaged metric.

`ACCURACY`

Accuracy is the fraction of predictions given the correct label. For multiclass this is a globally micro-averaged metric.

`F1_SCORE`

The F1 score is an average of recall and precision. For multiclass this is a macro-averaged metric.

`LOG_LOSS`

Logarithmic Loss. For multiclass this is a macro-averaged metric.

`ROC_AUC`

Area Under an ROC Curve. For multiclass this is a macro-averaged metric.

`DAVIES_BOULDIN_INDEX`

Davies-Bouldin Index.

`MEAN_AVERAGE_PRECISION`

Mean Average Precision.

`NORMALIZED_DISCOUNTED_CUMULATIVE_GAIN`

Normalized Discounted Cumulative Gain.

`AVERAGE_RANK`

Average Rank.

### EncodingMethod

Supported encoding methods for categorical features.

Enums

`ENCODING_METHOD_UNSPECIFIED`

Unspecified encoding method.

`ONE_HOT_ENCODING`

Applies one-hot encoding.

`LABEL_ENCODING`

Applies label encoding.

`DUMMY_ENCODING`

Applies dummy encoding.

### ColorSpace

Enums for color space, used for processing images in Object Table. See more details at <https://www.tensorflow.org/io/tutorials/colorspace> .

Enums

`COLOR_SPACE_UNSPECIFIED`

Unspecified color space

`RGB`

RGB

`HSV`

HSV

`YIQ`

YIQ

`YUV`

YUV

`GRAYSCALE`

GRAYSCALE

### PcaSolver

Enums for supported PCA solvers.

Enums

`UNSPECIFIED`

Default value.

`FULL`

Full eigen-decoposition.

`RANDOMIZED`

Randomized SVD.

`AUTO`

Auto.

### ModelRegistry

Enums for supported model registries.

Enums

`MODEL_REGISTRY_UNSPECIFIED`

Default value.

`VERTEX_AI`

Vertex AI.

### ReservationAffinityType

Supported reservation affinity types to configure a Vertex AI resource.

Enums

`RESERVATION_AFFINITY_TYPE_UNSPECIFIED`

Default value.

`NO_RESERVATION`

No reservation.

`ANY_RESERVATION`

Any reservation.

`SPECIFIC_RESERVATION`

Specific reservation.

### TrialStatus

Current status of the trial.

Enums

`TRIAL_STATUS_UNSPECIFIED`

Default value.

`NOT_STARTED`

Scheduled but not started.

`RUNNING`

Running state.

`SUCCEEDED`

The trial succeeded.

`FAILED`

The trial failed.

`INFEASIBLE`

The trial is infeasible due to the invalid params.

`STOPPED_EARLY`

Trial stopped early because it's not promising.

### BiEngineMode

Indicates the type of BI Engine acceleration.

Enums

`ACCELERATION_MODE_UNSPECIFIED`

BiEngineMode type not specified.

`DISABLED`

BI Engine disabled the acceleration. bi\_engine\_reasons specifies a more detailed reason.

`PARTIAL`

Part of the query was accelerated using BI Engine. See bi\_engine\_reasons for why parts of the query were not accelerated.

`FULL`

All of the query was accelerated using BI Engine.

### BiEngineAccelerationMode

Indicates the type of BI Engine acceleration.

Enums

`BI_ENGINE_ACCELERATION_MODE_UNSPECIFIED`

BiEngineMode type not specified.

`BI_ENGINE_DISABLED`

BI Engine acceleration was attempted but disabled. bi\_engine\_reasons specifies a more detailed reason.

`PARTIAL_INPUT`

Some inputs were accelerated using BI Engine. See bi\_engine\_reasons for why parts of the query were not accelerated.

`FULL_INPUT`

All of the query inputs were accelerated using BI Engine.

`FULL_QUERY`

All of the query was accelerated using BI Engine.

### Code

Indicates the high-level reason for no/partial acceleration

Enums

`CODE_UNSPECIFIED`

BiEngineReason not specified.

`NO_RESERVATION`

No reservation available for BI Engine acceleration.

`INSUFFICIENT_RESERVATION`

Not enough memory available for BI Engine acceleration.

`UNSUPPORTED_SQL_TEXT`

This particular SQL text is not supported for acceleration by BI Engine.

`INPUT_TOO_LARGE`

Input too large for acceleration by BI Engine.

`OTHER_REASON`

Catch-all code for all other cases for partial or disabled acceleration.

`TABLE_EXCLUDED`

One or more tables were not eligible for BI Engine acceleration.

### IndexUsageMode

Indicates the type of search index usage in the entire search query. In this context, "usage" means that an index lookup is attempted to prune base table data, with effectiveness depending on the selectivity of the search term.

Enums

`INDEX_USAGE_MODE_UNSPECIFIED`

Index usage mode not specified.

`UNUSED`

No search indexes were used in the search query. See [`indexUnusedReasons`](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/Job#IndexUnusedReason) for detailed reasons.

`PARTIALLY_USED`

Part of the search query used search indexes. See [`indexUnusedReasons`](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/Job#IndexUnusedReason) for why other parts of the query did not use search indexes.

`FULLY_USED`

The entire search query used search indexes.

### Code

Indicates the high-level reason for the scenario when no search index was used.

Enums

`CODE_UNSPECIFIED`

Code not specified.

`INDEX_CONFIG_NOT_AVAILABLE`

Indicates the search index configuration has not been created.

`PENDING_INDEX_CREATION`

Indicates the search index creation has not been completed.

`BASE_TABLE_TRUNCATED`

Indicates the base table has been truncated (rows have been removed from table with TRUNCATE TABLE statement) since the last time the search index was refreshed.

`INDEX_CONFIG_MODIFIED`

Indicates the search index configuration has been changed since the last time the search index was refreshed.

`TIME_TRAVEL_QUERY`

Indicates the search query accesses data at a timestamp before the last time the search index was refreshed.

`NO_PRUNING_POWER`

Indicates the usage of search index will not contribute to any pruning improvement for the search function, e.g. when the search predicate is in a disjunction with other non-search predicates.

`UNINDEXED_SEARCH_FIELDS`

Indicates the search index does not cover all fields in the search function.

`UNSUPPORTED_SEARCH_PATTERN`

Indicates the search index does not support the given search query pattern.

`OPTIMIZED_WITH_MATERIALIZED_VIEW`

Indicates the query has been optimized by using a materialized view.

`SECURED_BY_DATA_MASKING`

Indicates the query has been secured by data masking, and thus search indexes are not applicable.

`MISMATCHED_TEXT_ANALYZER`

Indicates that the search index and the search function call do not have the same text analyzer.

`BASE_TABLE_TOO_SMALL`

Indicates the base table is too small (below a certain threshold). The index does not provide noticeable search performance gains when the base table is too small.

`BASE_TABLE_TOO_LARGE`

Indicates that the total size of indexed base tables in your organization exceeds your region's limit and the index is not used in the query. To index larger base tables, you can [use your own reservation](https://cloud.google.com/bigquery/docs/search-index#use_your_own_reservation) for index-management jobs.

`ESTIMATED_PERFORMANCE_GAIN_TOO_LOW`

Indicates that the estimated performance gain from using the search index is too low for the given search query.

`COLUMN_METADATA_INDEX_NOT_USED`

Indicates that the column metadata index (which the search index depends on) is not used. User can refer to the [column metadata index usage](https://cloud.google.com/bigquery/docs/metadata-indexing-managed-tables#view_column_metadata_index_usage) for more details on why it was not used.

`NOT_SUPPORTED_IN_STANDARD_EDITION`

Indicates that search indexes can not be used for search query with STANDARD edition.

`INDEX_SUPPRESSED_BY_FUNCTION_OPTION`

Indicates that an option in the search function that cannot make use of the index has been selected.

`QUERY_CACHE_HIT`

Indicates that the query was cached, and thus the search index was not used.

`STALE_INDEX`

The index cannot be used in the search query because it is stale.

`INTERNAL_ERROR`

Indicates an internal error that causes the search index to be unused.

`OTHER_REASON`

Indicates that the reason search indexes cannot be used in the query is not covered by any of the other IndexUnusedReason options.

### IndexUsageMode

Indicates the type of vector index usage in the entire vector search query.

Enums

`INDEX_USAGE_MODE_UNSPECIFIED`

Index usage mode not specified.

`UNUSED`

No vector indexes were used in the vector search query. See [`indexUnusedReasons`](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/Job#IndexUnusedReason) for detailed reasons.

`PARTIALLY_USED`

Part of the vector search query used vector indexes. See [`indexUnusedReasons`](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/Job#IndexUnusedReason) for why other parts of the query did not use vector indexes.

`FULLY_USED`

The entire vector search query used vector indexes.

### Code

Indicates the high-level reason for the scenario when stored columns cannot be used in the query.

Enums

`CODE_UNSPECIFIED`

Default value.

`STORED_COLUMNS_COVER_INSUFFICIENT`

If stored columns do not fully cover the columns.

`BASE_TABLE_HAS_RLS`

If the base table has RLS (Row Level Security).

`BASE_TABLE_HAS_CLS`

If the base table has CLS (Column Level Security).

`UNSUPPORTED_PREFILTER`

If the provided prefilter is not supported.

`INTERNAL_ERROR`

If an internal error is preventing stored columns from being used.

`OTHER_REASON`

Indicates that the reason stored columns cannot be used in the query is not covered by any of the other StoredColumnsUnusedReason options.

### RejectedReason

Reason why a materialized view was not chosen for a query. For more information, see [Understand why materialized views were rejected](https://cloud.google.com/bigquery/docs/materialized-views-use#understand-rejected) .

Enums

`REJECTED_REASON_UNSPECIFIED`

Default unspecified value.

`NO_DATA`

View has no cached data because it has not refreshed yet.

`COST`

The estimated cost of the view is more expensive than another view or the base table.

Note: The estimate cost might not match the billed cost.

`BASE_TABLE_TRUNCATED`

View has no cached data because a base table is truncated.

`BASE_TABLE_DATA_CHANGE`

View is invalidated because of a data change in one or more base tables. It could be any recent change if the [`maxStaleness`](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#Table.FIELDS.max_staleness) option is not set for the view, or otherwise any change outside of the staleness window.

`BASE_TABLE_PARTITION_EXPIRATION_CHANGE`

View is invalidated because a base table's partition expiration has changed.

`BASE_TABLE_EXPIRED_PARTITION`

View is invalidated because a base table's partition has expired.

`BASE_TABLE_INCOMPATIBLE_METADATA_CHANGE`

View is invalidated because a base table has an incompatible metadata change.

`TIME_ZONE`

View is invalidated because it was refreshed with a time zone other than that of the current job.

`OUT_OF_TIME_TRAVEL_WINDOW`

View is outside the time travel window.

`BASE_TABLE_FINE_GRAINED_SECURITY_POLICY`

View is inaccessible to the user because of a fine-grained security policy on one of its base tables.

`BASE_TABLE_TOO_STALE`

One of the view's base tables is too stale. For example, the cached metadata of a BigLake external table needs to be updated.

### UnusedReason

Reasons for not using metadata caching.

Enums

`UNUSED_REASON_UNSPECIFIED`

Unused reasons not specified.

`EXCEEDED_MAX_STALENESS`

Metadata cache was outside the table's maxStaleness.

`METADATA_CACHING_NOT_ENABLED`

Metadata caching feature is not enabled. [Update BigLake tables](https://docs.cloud.google.com/bigquery/docs/create-cloud-storage-table-biglake#update-biglake-tables) to enable the metadata caching.

`OTHER_REASON`

Other unknown reason.

### DisabledReason

Reason why incremental query results are/were not written by the query.

Enums

`DISABLED_REASON_UNSPECIFIED`

Disabled reason not specified.

`OTHER`

Incremental results are/were disabled for reasons not covered by the other enum values, e.g. runtime issues.

`UNSUPPORTED_OPERATOR`

Query includes an operation that is not supported.

### CloudProvider

The cloud provider hosting the object storage.

Enums

`CLOUD_PROVIDER_UNSPECIFIED`

Unspecified cloud provider.

`GCP`

Google Cloud Platform.

`AWS`

Amazon Web Services.

`AZURE`

Microsoft Azure.

### EvaluationKind

Describes how the job is evaluated.

Enums

`EVALUATION_KIND_UNSPECIFIED`

Default value.

`STATEMENT`

The statement appears directly in the script.

`EXPRESSION`

The statement evaluates an expression that appears in the script.

### ReservationEdition

The type of editions. Different features and behaviors are provided to different editions Capacity commitments and reservations are linked to editions.

Enums

`RESERVATION_EDITION_UNSPECIFIED`

Default value, which will be treated as ENTERPRISE.

`STANDARD`

Standard edition.

`ENTERPRISE`

Enterprise edition.

`ENTERPRISE_PLUS`

Enterprise Plus edition.

### Code

Indicates the high level reason why a job was created.

Enums

`CODE_UNSPECIFIED`

Reason is not specified.

`REQUESTED`

Job creation was requested.

`LONG_RUNNING`

The query request ran beyond a system defined timeout specified by the [timeoutMs field in the QueryRequest](https://cloud.google.com/bigquery/docs/reference/rest/v2/jobs/query#queryrequest) . As a result it was considered a long running operation for which a job was created.

`LARGE_RESULTS`

The results from the query cannot fit in the response.

`OTHER`

BigQuery has determined that the query needs to be executed as a Job.

### Tool Annotations

[Tool annotations](https://modelcontextprotocol.io/specification/latest/schema#toolannotations) are sent to MCP clients to describe the basic risk of a given tool. Most clients treat these hints as untrusted, but they can be used to decide when a confirmation prompt might be sent to a user.

Along with the title string, the following boolean hints are defined as follows:

  - `readOnlyHint` : If true, the tool doesn't modify its environment. Default: false.
  - `destructiveHint` : If true, then the tool can perform destructive actions. If false, then the tool can only perform additive actions. Default: true.
  - `idempotentHint` : If true, then calling the tool repeatedly with the same arguments will have no additional effect on its environment. Default: false.
  - `openWorldHint` : If true, then the tool can interact with an 'open world' of external entities. If false, then the tool can only interact with internal entities. For example, a web search tool would be open world, while a memory tool would not be open world.

Destructive Hint: ✅ | Idempotent Hint: ✅ | Read Only Hint: ❌ | Open World Hint: ❌
