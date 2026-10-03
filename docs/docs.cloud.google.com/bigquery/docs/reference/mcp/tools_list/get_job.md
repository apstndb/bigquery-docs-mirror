---
name: documents/docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_job
uri: https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_job
title: 'MCP Tools Reference: bigquery.googleapis.com'
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

## Tool: `get_job`

Get information and status about a BigQuery job.

Use this tool to check the status, statistics, or configuration of a job using its `job_id` .

The following code sample shows how to use `curl` to call the `get_job` MCP tool.

**Curl Request**

```
curl --location 'https://bigquery.googleapis.com/mcp' \
--header 'content-type: application/json' \
--header 'accept: application/json, text/event-stream' \
--data '{
  "method": "tools/call",
  "params": {
    "name": "get_job",
    "arguments": {
      // Provide these details according to the MCP tool specification.
    }
  },
  "jsonrpc": "2.0",
  "id": 1
}'
```

## Input Schema

Request for getting information about a job.

### GetJobRequest

**JSON representation**

```
{
  "projectId": string,
  "jobId": string,
  "location": string
}
```

| Fields      |                                                        |
|-------------|--------------------------------------------------------|
| `projectId` | `string` Required. Project ID of the requested job.    |
| `jobId`     | `string` Required. Job ID of the requested job.        |
| `location`  | `string` Optional. The geographic location of the job. |

## Output Schema

### Job

**JSON representation**

```
{
  "kind": string,
  "etag": string,
  "id": string,
  "selfLink": string,
  "user_email": string,
  "configuration": {
    object (JobConfiguration)
  },
  "jobReference": {
    object (JobReference)
  },
  "statistics": {
    object (JobStatistics)
  },
  "status": {
    object (JobStatus)
  },
  "principal_subject": string,
  "jobCreationReason": {
    object (JobCreationReason)
  }
}
```

| Fields              |                                                                                                                                                                                                                                                               |
|---------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `kind`              | `string` Output only. The type of the resource.                                                                                                                                                                                                               |
| `etag`              | `string` Output only. A hash of this resource.                                                                                                                                                                                                                |
| `id`                | `string` Output only. Opaque ID field of the job.                                                                                                                                                                                                             |
| `selfLink`          | `string` Output only. A URL that can be used to access the resource again.                                                                                                                                                                                    |
| `user_email`        | `string` Output only. Email address of the user who ran the job.                                                                                                                                                                                              |
| `configuration`     | `object ( `[`JobConfiguration`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.JobConfiguration)` )` Required. Describes the job configuration.                                                                |
| `jobReference`      | `object ( `[`JobReference`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.JobReference)` )` Optional. Reference describing the unique-per-user name of the job.                                               |
| `statistics`        | `object ( `[`JobStatistics`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.JobStatistics)` )` Output only. Information about the job, including starting time and ending time of the job.                     |
| `status`            | `object ( `[`JobStatus`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.JobStatus)` )` Output only. The status of this job. Examine this value when polling an asynchronous job to see if the job is complete. |
| `principal_subject` | `string` Output only. \[Full-projection-only\] String representation of identity of requesting party. Populated for both first- and third-party identities. Only present for APIs that support third-party identities.                                        |
| `jobCreationReason` | `object ( `[`JobCreationReason`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.JobCreationReason)` )` Output only. The reason why a Job was created.                                                          |

### JobConfiguration

**JSON representation**

```
{
  "jobType": string,
  "query": {
    object (JobConfigurationQuery)
  },
  "load": {
    object (JobConfigurationLoad)
  },
  "copy": {
    object (JobConfigurationTableCopy)
  },
  "extract": {
    object (JobConfigurationExtract)
  },
  "dryRun": boolean,
  "jobTimeoutMs": string,
  "labels": {
    string: string,
    ...
  },

  // Union field _max_slots can be only one of the following:
  "maxSlots": integer
  // End of list of possible types for union field _max_slots.

  // Union field _reservation can be only one of the following:
  "reservation": string
  // End of list of possible types for union field _reservation.
}
```

| Fields                                                                        |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
|-------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `jobType`                                                                     | `string` Output only. The type of the job. Can be QUERY, LOAD, EXTRACT, COPY or UNKNOWN.                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| `query`                                                                       | `object ( `[`JobConfigurationQuery`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.JobConfigurationQuery)` )` \[Pick one\] Configures a query job.                                                                                                                                                                                                                                                                                                                                                     |
| `load`                                                                        | `object ( `[`JobConfigurationLoad`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.JobConfigurationLoad)` )` \[Pick one\] Configures a load job.                                                                                                                                                                                                                                                                                                                                                        |
| `copy`                                                                        | `object ( `[`JobConfigurationTableCopy`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.JobConfigurationTableCopy)` )` \[Pick one\] Copies a table.                                                                                                                                                                                                                                                                                                                                                     |
| `extract`                                                                     | `object ( `[`JobConfigurationExtract`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.JobConfigurationExtract)` )` \[Pick one\] Configures an extract job.                                                                                                                                                                                                                                                                                                                                              |
| `dryRun`                                                                      | `boolean` Optional. If set, don't actually run this job. A valid query will return a mostly empty response with some processing statistics, while an invalid query will return the same error it would if it wasn't a dry run. Behavior of non-query jobs is undefined.                                                                                                                                                                                                                                                                                |
| `jobTimeoutMs`                                                                | `string ( `[`Int64Value`](https://developers.google.com/discovery/v1/type-format)` format)` Optional. Job timeout in milliseconds relative to the job creation time. If this time limit is exceeded, BigQuery attempts to stop the job, but might not always succeed in canceling it before the job completes. For example, a job that takes more than 60 seconds to complete has a better chance of being stopped than a job that takes 10 seconds to complete.                                                                                       |
| `labels`                                                                      | `map (key: string, value: string)` The labels associated with this job. You can use these to organize and group your jobs. Label keys and values can be no longer than 63 characters, can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. Label values are optional. Label keys must start with a letter and each label in the list must have a different key. An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` . |
| Union field `_max_slots` . `_max_slots` can be only one of the following:     |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `maxSlots`                                                                    | `integer` Optional. A target limit on the rate of slot consumption by this job. If set to a value \> 0, BigQuery will attempt to limit the rate of slot consumption by this job to keep it below the configured limit, even if the job is eligible for more slots based on fair scheduling. The unused slots will be available for other jobs and queries to use. Note: This feature is not yet generally available.                                                                                                                                   |
|                                                                               |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| Union field `_reservation` . `_reservation` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `reservation`                                                                 | `string` Optional. The reservation that job would use. User can specify a reservation to execute the job. If reservation is not set, reservation is determined based on the rules defined by the reservation assignments. The expected format is `projects/{project}/locations/{location}/reservations/{reservation}` . Forces the query to use on-demand billing when set to `none` , which requires the project or organization to have `reservation_override_mode` set to `ALLOW_ANY_OVERRIDE` .                                                    |
|                                                                               |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |

### JobConfigurationQuery

**JSON representation**

```
{
  "query": string,
  "destinationTable": {
    object (TableReference)
  },
  "tableDefinitions": {
    string: {
      object (ExternalDataConfiguration)
    },
    ...
  },
  "userDefinedFunctionResources": [
    {
      object (UserDefinedFunctionResource)
    }
  ],
  "createDisposition": string,
  "writeDisposition": string,
  "defaultDataset": {
    object (DatasetReference)
  },
  "priority": string,
  "preserveNulls": boolean,
  "allowLargeResults": boolean,
  "useQueryCache": boolean,
  "flattenResults": boolean,
  "maximumBillingTier": integer,
  "maximumBytesBilled": string,
  "useLegacySql": boolean,
  "parameterMode": string,
  "queryParameters": [
    {
      object (QueryParameter)
    }
  ],
  "schemaUpdateOptions": [
    string
  ],
  "timePartitioning": {
    object (TimePartitioning)
  },
  "rangePartitioning": {
    object (RangePartitioning)
  },
  "clustering": {
    object (Clustering)
  },
  "destinationEncryptionConfiguration": {
    object (EncryptionConfiguration)
  },
  "scriptOptions": {
    object (ScriptOptions)
  },
  "connectionProperties": [
    {
      object (ConnectionProperty)
    }
  ],
  "createSession": boolean,
  "continuous": boolean,
  "writeIncrementalResults": boolean,
  "secureContext": {
    object (SecureContext)
  },

  // Union field _system_variables can be only one of the following:
  "systemVariables": {
    object (SystemVariables)
  }
  // End of list of possible types for union field _system_variables.
}
```

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
<td><code>query</code></td>
<td><p><code>string</code></p>
<p>[Required] SQL query text to execute. The useLegacySql field can be used to indicate whether the query uses legacy SQL or GoogleSQL.</p></td>
</tr>
<tr class="even">
<td><code>destinationTable</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_dataset_info#Output.Schema.TableReference"><code>TableReference</code></a><code> )</code></p>
<p>Optional. Describes the table where the query results should be stored. This property must be set for large results that exceed the maximum response size. For queries that produce anonymous (cached) results, this field will be populated by BigQuery.</p></td>
</tr>
<tr class="odd">
<td><code>tableDefinitions</code></td>
<td><p><code>map (key: string, value: object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.ExternalDataConfiguration"><code>ExternalDataConfiguration</code></a><code> ))</code></p>
<p>Optional. You can specify external table definitions, which operate as ephemeral tables that can be queried. These definitions are configured using a JSON map, where the string key represents the table identifier, and the value is the corresponding external data configuration object.</p>
<p>An object containing a list of <code>"key": value</code> pairs. Example: <code>{ "name": "wrench", "mass": "1.3kg", "count": "3" }</code> .</p></td>
</tr>
<tr class="even">
<td><code>userDefinedFunctionResources[]</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.UserDefinedFunctionResource"><code>UserDefinedFunctionResource</code></a><code> )</code></p>
<p>Describes user-defined function resources used in the query.</p></td>
</tr>
<tr class="odd">
<td><code>createDisposition</code></td>
<td><p><code>string</code></p>
<p>Optional. Specifies whether the job is allowed to create new tables. The following values are supported:</p>
<ul>
<li>CREATE_IF_NEEDED: If the table does not exist, BigQuery creates the table.</li>
<li>CREATE_NEVER: The table must already exist. If it does not, a 'notFound' error is returned in the job result.</li>
</ul>
<p>The default value is CREATE_IF_NEEDED. Creation, truncation and append actions occur as one atomic update upon job completion.</p></td>
</tr>
<tr class="even">
<td><code>writeDisposition</code></td>
<td><p><code>string</code></p>
<p>Optional. Specifies the action that occurs if the destination table already exists. The following values are supported:</p>
<ul>
<li>WRITE_TRUNCATE: If the table already exists, BigQuery overwrites the data, removes the constraints, and uses the schema from the query result.</li>
<li>WRITE_TRUNCATE_DATA: If the table already exists, BigQuery overwrites the data, but keeps the constraints and schema of the existing table.</li>
<li>WRITE_APPEND: If the table already exists, BigQuery appends the data to the table.</li>
<li>WRITE_EMPTY: If the table already exists and contains data, a 'duplicate' error is returned in the job result.</li>
</ul>
<p>The default value is WRITE_EMPTY. Each action is atomic and only occurs if BigQuery is able to complete the job successfully. Creation, truncation and append actions occur as one atomic update upon job completion.</p></td>
</tr>
<tr class="odd">
<td><code>defaultDataset</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_dataset_info#Output.Schema.DatasetReference"><code>DatasetReference</code></a><code> )</code></p>
<p>Optional. Specifies the default dataset to use for unqualified table names in the query. This setting does not alter behavior of unqualified dataset names. Setting the system variable <code>@@dataset_id</code> achieves the same behavior. See <a href="https://cloud.google.com/bigquery/docs/reference/system-variables">https://cloud.google.com/bigquery/docs/reference/system-variables</a> for more information on system variables.</p></td>
</tr>
<tr class="even">
<td><code>priority</code></td>
<td><p><code>string</code></p>
<p>Optional. Specifies a priority for the query. Possible values include INTERACTIVE and BATCH. The default value is INTERACTIVE.</p></td>
</tr>
<tr class="odd">
<td><code>preserveNulls</code></td>
<td><p><code>boolean</code></p>
<p>[Deprecated] This property is deprecated.</p></td>
</tr>
<tr class="even">
<td><code>allowLargeResults</code></td>
<td><p><code>boolean</code></p>
<p>Optional. If true and query uses legacy SQL dialect, allows the query to produce arbitrarily large result tables at a slight cost in performance. Requires destinationTable to be set. For GoogleSQL queries, this flag is ignored and large results are always allowed. However, you must still set destinationTable when result size exceeds the allowed maximum response size.</p></td>
</tr>
<tr class="odd">
<td><code>useQueryCache</code></td>
<td><p><code>boolean</code></p>
<p>Optional. Whether to look for the result in the query cache. The query cache is a best-effort cache that will be flushed whenever tables in the query are modified. Moreover, the query cache is only available when a query does not have a destination table specified. The default value is true.</p></td>
</tr>
<tr class="even">
<td><code>flattenResults</code></td>
<td><p><code>boolean</code></p>
<p>Optional. If true and query uses legacy SQL dialect, flattens all nested and repeated fields in the query results. allowLargeResults must be true if this is set to false. For GoogleSQL queries, this flag is ignored and results are never flattened.</p></td>
</tr>
<tr class="odd">
<td><code>maximumBillingTier</code></td>
<td><p><code>integer</code></p>
<p>Optional. [Deprecated] Maximum billing tier allowed for this query. The billing tier controls the amount of compute resources allotted to the query, and multiplies the on-demand cost of the query accordingly. A query that runs within its allotted resources will succeed and indicate its billing tier in statistics.query.billingTier, but if the query exceeds its allotted resources, it will fail with billingTierLimitExceeded. WARNING: The billed byte amount can be multiplied by an amount up to this number! Most users should not need to alter this setting, and we recommend that you avoid introducing new uses of it.</p></td>
</tr>
<tr class="even">
<td><code>maximumBytesBilled</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>Int64Value</code></a><code> format)</code></p>
<p>Limits the bytes billed for this job. Queries that will have bytes billed beyond this limit will fail (without incurring a charge). If unspecified, this will be set to your project default.</p></td>
</tr>
<tr class="odd">
<td><code>useLegacySql</code></td>
<td><p><code>boolean</code></p>
<p>Optional. Specifies whether to use BigQuery's legacy SQL dialect for this query. The default value is true. If set to false, the query uses BigQuery's <a href="https://docs.cloud.google.com/bigquery/docs/introduction-sql">GoogleSQL</a> .</p>
<p>When useLegacySql is set to false, the value of flattenResults is ignored; query will be run as if flattenResults is false.</p></td>
</tr>
<tr class="even">
<td><code>parameterMode</code></td>
<td><p><code>string</code></p>
<p>GoogleSQL only. Set to POSITIONAL to use positional (?) query parameters or to NAMED to use named (@myparam) query parameters in this query.</p></td>
</tr>
<tr class="odd">
<td><code>queryParameters[]</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.QueryParameter"><code>QueryParameter</code></a><code> )</code></p>
<p>Query parameters for GoogleSQL queries.</p></td>
</tr>
<tr class="even">
<td><code>schemaUpdateOptions[]</code></td>
<td><p><code>string</code></p>
<p>Allows the schema of the destination table to be updated as a side effect of the query job. Schema update options are supported in three cases: when writeDisposition is WRITE_APPEND; when writeDisposition is WRITE_TRUNCATE_DATA; when writeDisposition is WRITE_TRUNCATE and the destination table is a partition of a table, specified by partition decorators. For normal tables, WRITE_TRUNCATE will always overwrite the schema. One or more of the following values are specified:</p>
<ul>
<li>ALLOW_FIELD_ADDITION: allow adding a nullable field to the schema.</li>
<li>ALLOW_FIELD_RELAXATION: allow relaxing a required field in the original schema to nullable.</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>timePartitioning</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.TimePartitioning"><code>TimePartitioning</code></a><code> )</code></p>
<p>Time-based partitioning specification for the destination table. Only one of timePartitioning and rangePartitioning should be specified.</p></td>
</tr>
<tr class="even">
<td><code>rangePartitioning</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.RangePartitioning"><code>RangePartitioning</code></a><code> )</code></p>
<p>Range partitioning specification for the destination table. Only one of timePartitioning and rangePartitioning should be specified.</p></td>
</tr>
<tr class="odd">
<td><code>clustering</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.Clustering"><code>Clustering</code></a><code> )</code></p>
<p>Clustering specification for the destination table.</p></td>
</tr>
<tr class="even">
<td><code>destinationEncryptionConfiguration</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_dataset_info#Output.Schema.EncryptionConfiguration"><code>EncryptionConfiguration</code></a><code> )</code></p>
<p>Custom encryption configuration (e.g., Cloud KMS keys)</p></td>
</tr>
<tr class="odd">
<td><code>scriptOptions</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.ScriptOptions"><code>ScriptOptions</code></a><code> )</code></p>
<p>Options controlling the execution of scripts.</p></td>
</tr>
<tr class="even">
<td><code>connectionProperties[]</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.ConnectionProperty"><code>ConnectionProperty</code></a><code> )</code></p>
<p>Connection properties which can modify the query behavior.</p></td>
</tr>
<tr class="odd">
<td><code>createSession</code></td>
<td><p><code>boolean</code></p>
<p>If this property is true, the job creates a new session using a randomly generated session_id. To continue using a created session with subsequent queries, pass the existing session identifier as a <code>ConnectionProperty</code> value. The session identifier is returned as part of the <code>SessionInfo</code> message within the query statistics.</p>
<p>The new session's location will be set to <code>Job.JobReference.location</code> if it is present, otherwise it's set to the default location based on existing routing logic.</p></td>
</tr>
<tr class="even">
<td><code>continuous</code></td>
<td><p><code>boolean</code></p>
<p>Optional. Whether to run the query as continuous or a regular query. Continuous query is currently in experimental stage and not ready for general usage.</p></td>
</tr>
<tr class="odd">
<td><code>writeIncrementalResults</code></td>
<td><p><code>boolean</code></p>
<p>Optional. This is only supported for a SELECT query using a temporary table. If set, the query is allowed to write results incrementally to the temporary result table. This may incur a performance penalty. This option cannot be used with Legacy SQL. This feature is not yet available.</p></td>
</tr>
<tr class="even">
<td><code>secureContext</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.SecureContext"><code>SecureContext</code></a><code> )</code></p>
<p>Optional. A set of key-value pairs representing the secure context. This can be used to pass sensitive or context-specific information. They can be retrieved via the SECURE_CONTEXT() function and used to modify the run-time behavior of a query.</p></td>
</tr>
<tr class="odd">
<td><p>Union field <code>_system_variables</code> .</p>
<p><code>_system_variables</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="even">
<td><code>systemVariables</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.SystemVariables"><code>SystemVariables</code></a><code> )</code></p>
<p>Output only. System variables for GoogleSQL queries. A system variable is output if the variable is settable and its value differs from the system default. "@@" prefix is not included in the name of the System variables.</p></td>
</tr>
<tr class="odd">
<td></td>
<td></td>
</tr>
</tbody>
</table>

### TableReference

**JSON representation**

```
{
  "projectId": string,
  "datasetId": string,
  "tableId": string
}
```

| Fields      |                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
|-------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `projectId` | `string` Required. The ID of the project containing this table.                                                                                                                                                                                                                                                                                                                                                                                                              |
| `datasetId` | `string` Required. The ID of the dataset containing this table.                                                                                                                                                                                                                                                                                                                                                                                                              |
| `tableId`   | `string` Required. The ID of the table. The ID can contain Unicode characters in category L (letter), M (mark), N (number), Pc (connector, including underscore), Pd (dash), and Zs (space). For more information, see [General Category](https://wikipedia.org/wiki/Unicode_character_property#General_Category) . The maximum length is 1,024 characters. Certain operations allow suffixing of the table ID with a partition decorator, such as `sample_table$20190123` . |

### ExternalTableDefinitionsEntry

**JSON representation**

```
{
  "key": string,
  "value": {
    object (ExternalDataConfiguration)
  }
}
```

| Fields  |                                                                                                                                                                           |
|---------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `key`   | `string`                                                                                                                                                                  |
| `value` | `object ( `[`ExternalDataConfiguration`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.ExternalDataConfiguration)` )` |

### ExternalDataConfiguration

**JSON representation**

```
{
  "sourceUris": [
    string
  ],
  "fileSetSpecType": enum (FileSetSpecType),
  "schema": {
    object (TableSchema)
  },
  "sourceFormat": string,
  "maxBadRecords": integer,
  "autodetect": boolean,
  "ignoreUnknownValues": boolean,
  "compression": string,
  "csvOptions": {
    object (CsvOptions)
  },
  "jsonOptions": {
    object (JsonOptions)
  },
  "bigtableOptions": {
    object (BigtableOptions)
  },
  "googleSheetsOptions": {
    object (GoogleSheetsOptions)
  },
  "hivePartitioningOptions": {
    object (HivePartitioningOptions)
  },
  "connectionId": string,
  "decimalTargetTypes": [
    enum (DecimalTargetType)
  ],
  "avroOptions": {
    object (AvroOptions)
  },
  "jsonExtension": enum (JsonExtension),
  "parquetOptions": {
    object (ParquetOptions)
  },
  "referenceFileSchemaUri": string,
  "metadataCacheMode": enum (MetadataCacheMode),
  "timestampTargetPrecision": [
    integer
  ],

  // Union field _object_metadata can be only one of the following:
  "objectMetadata": enum (ObjectMetadata)
  // End of list of possible types for union field _object_metadata.

  // Union field _time_zone can be only one of the following:
  "timeZone": string
  // End of list of possible types for union field _time_zone.

  // Union field _date_format can be only one of the following:
  "dateFormat": string
  // End of list of possible types for union field _date_format.

  // Union field _datetime_format can be only one of the following:
  "datetimeFormat": string
  // End of list of possible types for union field _datetime_format.

  // Union field _time_format can be only one of the following:
  "timeFormat": string
  // End of list of possible types for union field _time_format.

  // Union field _timestamp_format can be only one of the following:
  "timestampFormat": string
  // End of list of possible types for union field _timestamp_format.
}
```

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
<td><code>sourceUris[]</code></td>
<td><p><code>string</code></p>
<p>[Required] The fully-qualified URIs that point to your data in Google Cloud. For Google Cloud Storage URIs: Each URI can contain one '*' wildcard character and it must come after the 'bucket' name. Size limits related to load jobs apply to external data sources. For Google Cloud Bigtable URIs: Exactly one URI can be specified and it has be a fully specified and valid HTTPS URL for a Google Cloud Bigtable table. For Google Cloud Datastore backups, exactly one URI can be specified. Also, the '*' wildcard character is not allowed.</p></td>
</tr>
<tr class="even">
<td><code>fileSetSpecType</code></td>
<td><p><code>enum ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.FileSetSpecType"><code>FileSetSpecType</code></a><code> )</code></p>
<p>Optional. Specifies how source URIs are interpreted for constructing the file set to load. By default source URIs are expanded against the underlying storage. Other options include specifying manifest files. Only applicable to object storage systems.</p></td>
</tr>
<tr class="odd">
<td><code>schema</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.TableSchema"><code>TableSchema</code></a><code> )</code></p>
<p>Optional. The schema for the data. Schema is required for CSV and JSON formats if autodetect is not on. Schema is disallowed for Google Cloud Bigtable, Cloud Datastore backups, Avro, ORC and Parquet formats.</p></td>
</tr>
<tr class="even">
<td><code>sourceFormat</code></td>
<td><p><code>string</code></p>
<p>[Required] The data format. For CSV files, specify "CSV". For Google sheets, specify "GOOGLE_SHEETS". For newline-delimited JSON, specify "NEWLINE_DELIMITED_JSON". For Avro files, specify "AVRO". For Google Cloud Datastore backups, specify "DATASTORE_BACKUP". For Apache Iceberg tables, specify "ICEBERG". For ORC files, specify "ORC". For Parquet files, specify "PARQUET". [Beta] For Google Cloud Bigtable, specify "BIGTABLE".</p></td>
</tr>
<tr class="odd">
<td><code>maxBadRecords</code></td>
<td><p><code>integer</code></p>
<p>Optional. The maximum number of bad records that BigQuery can ignore when reading data. If the number of bad records exceeds this value, an invalid error is returned in the job result. The default value is 0, which requires that all records are valid. This setting is ignored for Google Cloud Bigtable, Google Cloud Datastore backups, Avro, ORC and Parquet formats.</p></td>
</tr>
<tr class="even">
<td><code>autodetect</code></td>
<td><p><code>boolean</code></p>
<p>Try to detect schema and format options automatically. Any option specified explicitly will be honored.</p></td>
</tr>
<tr class="odd">
<td><code>ignoreUnknownValues</code></td>
<td><p><code>boolean</code></p>
<p>Optional. Indicates if BigQuery should allow extra values that are not represented in the table schema. If true, the extra values are ignored. If false, records with extra columns are treated as bad records, and if there are too many bad records, an invalid error is returned in the job result. The default value is false. The sourceFormat property determines what BigQuery treats as an extra value: CSV: Trailing columns JSON: Named values that don't match any column names Google Cloud Bigtable: This setting is ignored. Google Cloud Datastore backups: This setting is ignored. Avro: This setting is ignored. ORC: This setting is ignored. Parquet: This setting is ignored.</p></td>
</tr>
<tr class="even">
<td><code>compression</code></td>
<td><p><code>string</code></p>
<p>Optional. The compression type of the data source. Possible values include GZIP and NONE. The default value is NONE. This setting is ignored for Google Cloud Bigtable, Google Cloud Datastore backups, Avro, ORC and Parquet formats. An empty string is an invalid value.</p></td>
</tr>
<tr class="odd">
<td><code>csvOptions</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.CsvOptions"><code>CsvOptions</code></a><code> )</code></p>
<p>Optional. Additional properties to set if sourceFormat is set to CSV.</p></td>
</tr>
<tr class="even">
<td><code>jsonOptions</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.JsonOptions"><code>JsonOptions</code></a><code> )</code></p>
<p>Optional. Additional properties to set if sourceFormat is set to JSON.</p></td>
</tr>
<tr class="odd">
<td><code>bigtableOptions</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.BigtableOptions"><code>BigtableOptions</code></a><code> )</code></p>
<p>Optional. Additional options if sourceFormat is set to BIGTABLE.</p></td>
</tr>
<tr class="even">
<td><code>googleSheetsOptions</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.GoogleSheetsOptions"><code>GoogleSheetsOptions</code></a><code> )</code></p>
<p>Optional. Additional options if sourceFormat is set to GOOGLE_SHEETS.</p></td>
</tr>
<tr class="odd">
<td><code>hivePartitioningOptions</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.HivePartitioningOptions"><code>HivePartitioningOptions</code></a><code> )</code></p>
<p>Optional. When set, configures hive partitioning support. Not all storage formats support hive partitioning -- requesting hive partitioning on an unsupported format will lead to an error, as will providing an invalid specification.</p></td>
</tr>
<tr class="even">
<td><code>connectionId</code></td>
<td><p><code>string</code></p>
<p>Optional. The connection specifying the credentials to be used to read external storage, such as Azure Blob, Cloud Storage, or S3. The connection_id can have the form <code>{project_id}.{location_id};{connection_id}</code> or <code>projects/{project_id}/locations/{location_id}/connections/{connection_id}</code> .</p></td>
</tr>
<tr class="odd">
<td><code>decimalTargetTypes[]</code></td>
<td><p><code>enum ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.DecimalTargetType"><code>DecimalTargetType</code></a><code> )</code></p>
<p>Defines the list of possible SQL data types to which the source decimal values are converted. This list and the precision and the scale parameters of the decimal field determine the target type. In the order of NUMERIC, BIGNUMERIC, and STRING, a type is picked if it is in the specified list and if it supports the precision and the scale. STRING supports all precision and scale values. If none of the listed types supports the precision and the scale, the type supporting the widest range in the specified list is picked, and if a value exceeds the supported range when reading the data, an error will be thrown.</p>
<p>Example: Suppose the value of this field is ["NUMERIC", "BIGNUMERIC"]. If (precision,scale) is:</p>
<ul>
<li>(38,9) -&gt; NUMERIC;</li>
<li>(39,9) -&gt; BIGNUMERIC (NUMERIC cannot hold 30 integer digits);</li>
<li>(38,10) -&gt; BIGNUMERIC (NUMERIC cannot hold 10 fractional digits);</li>
<li>(76,38) -&gt; BIGNUMERIC;</li>
<li>(77,38) -&gt; BIGNUMERIC (error if value exceeds supported range).</li>
</ul>
<p>This field cannot contain duplicate types. The order of the types in this field is ignored. For example, ["BIGNUMERIC", "NUMERIC"] is the same as ["NUMERIC", "BIGNUMERIC"] and NUMERIC always takes precedence over BIGNUMERIC.</p>
<p>Defaults to ["NUMERIC", "STRING"] for ORC and ["NUMERIC"] for the other file formats.</p></td>
</tr>
<tr class="even">
<td><code>avroOptions</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.AvroOptions"><code>AvroOptions</code></a><code> )</code></p>
<p>Optional. Additional properties to set if sourceFormat is set to AVRO.</p></td>
</tr>
<tr class="odd">
<td><code>jsonExtension</code></td>
<td><p><code>enum ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.JsonExtension"><code>JsonExtension</code></a><code> )</code></p>
<p>Optional. Load option to be used together with source_format newline-delimited JSON to indicate that a variant of JSON is being loaded. To load newline-delimited GeoJSON, specify GEOJSON (and source_format must be set to NEWLINE_DELIMITED_JSON).</p></td>
</tr>
<tr class="even">
<td><code>parquetOptions</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.ParquetOptions"><code>ParquetOptions</code></a><code> )</code></p>
<p>Optional. Additional properties to set if sourceFormat is set to PARQUET.</p></td>
</tr>
<tr class="odd">
<td><code>referenceFileSchemaUri</code></td>
<td><p><code>string</code></p>
<p>Optional. When creating an external table, the user can provide a reference file with the table schema. This is enabled for the following formats: AVRO, PARQUET, ORC.</p></td>
</tr>
<tr class="even">
<td><code>metadataCacheMode</code></td>
<td><p><code>enum ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.MetadataCacheMode"><code>MetadataCacheMode</code></a><code> )</code></p>
<p>Optional. Metadata Cache Mode for the table. Set this to enable caching of metadata from external data source.</p></td>
</tr>
<tr class="odd">
<td><code>timestampTargetPrecision[]</code></td>
<td><p><code>integer</code></p>
<p>Precisions (maximum number of total digits in base 10) for seconds of TIMESTAMP types that are allowed to the destination table for autodetection mode.</p>
<p>Available for the formats: CSV, PARQUET, AVRO, and Iceberg External Table.</p>
<p>Possible values include: Not Specified, [], or [6]: timestamp(6) for all auto detected TIMESTAMP columns [6, 12]: timestamp(6) for all auto detected TIMESTAMP columns that have less than 6 digits of subseconds. timestamp(12) for all auto detected TIMESTAMP columns that have more than 6 digits of subseconds. [12]: timestamp(12) for all auto detected TIMESTAMP columns.</p>
<p>The order of the elements in this array is ignored. Inputs that have higher precision than the highest target precision in this array will be truncated.</p></td>
</tr>
<tr class="even">
<td><p>Union field <code>_object_metadata</code> .</p>
<p><code>_object_metadata</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="odd">
<td><code>objectMetadata</code></td>
<td><p><code>enum ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.ObjectMetadata"><code>ObjectMetadata</code></a><code> )</code></p>
<p>Optional. ObjectMetadata is used to create Object Tables. Object Tables contain a listing of objects (with their metadata) found at the source_uris. If ObjectMetadata is set, source_format should be omitted.</p>
<p>Currently SIMPLE is the only supported Object Metadata type.</p></td>
</tr>
<tr class="even">
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p>Union field <code>_time_zone</code> .</p>
<p><code>_time_zone</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="even">
<td><code>timeZone</code></td>
<td><p><code>string</code></p>
<p>Optional. Time zone used when parsing timestamp values that do not have specific time zone information (e.g. 2024-04-20 12:34:56). The expected format is a IANA timezone string (e.g. America/Los_Angeles).</p></td>
</tr>
<tr class="odd">
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p>Union field <code>_date_format</code> .</p>
<p><code>_date_format</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="odd">
<td><code>dateFormat</code></td>
<td><p><code>string</code></p>
<p>Optional. Format used to parse DATE values. Supports C-style and SQL-style values.</p></td>
</tr>
<tr class="even">
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p>Union field <code>_datetime_format</code> .</p>
<p><code>_datetime_format</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="even">
<td><code>datetimeFormat</code></td>
<td><p><code>string</code></p>
<p>Optional. Format used to parse DATETIME values. Supports C-style and SQL-style values.</p></td>
</tr>
<tr class="odd">
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p>Union field <code>_time_format</code> .</p>
<p><code>_time_format</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="odd">
<td><code>timeFormat</code></td>
<td><p><code>string</code></p>
<p>Optional. Format used to parse TIME values. Supports C-style and SQL-style values.</p></td>
</tr>
<tr class="even">
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p>Union field <code>_timestamp_format</code> .</p>
<p><code>_timestamp_format</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="even">
<td><code>timestampFormat</code></td>
<td><p><code>string</code></p>
<p>Optional. Format used to parse TIMESTAMP values. Supports C-style and SQL-style values.</p></td>
</tr>
<tr class="odd">
<td></td>
<td></td>
</tr>
</tbody>
</table>

### TableSchema

**JSON representation**

```
{
  "fields": [
    {
      object (TableFieldSchema)
    }
  ],
  "foreignTypeInfo": {
    object (ForeignTypeInfo)
  }
}
```

| Fields            |                                                                                                                                                                                                                                                                                        |
|-------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `fields[]`        | `object ( `[`TableFieldSchema`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.TableFieldSchema)` )` Describes the fields in a table.                                                                                               |
| `foreignTypeInfo` | `object ( `[`ForeignTypeInfo`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.ForeignTypeInfo)` )` Optional. Specifies metadata of the foreign data type definition in field schema ( `TableFieldSchema.foreign_type_definition` ). |

### TableFieldSchema

**JSON representation**

```
{
  "name": string,
  "type": string,
  "mode": string,
  "fields": [
    {
      object (TableFieldSchema)
    }
  ],
  "description": string,
  "policyTags": {
    object (PolicyTagList)
  },
  "dataGovernanceTagsInfo": {
    object (DataGovernanceTagsInfo)
  },
  "dataPolicies": [
    {
      object (DataPolicyOption)
    }
  ],
  "dataPolicyList": {
    object (DataPolicyList)
  },
  "maxLength": string,
  "precision": string,
  "scale": string,
  "timestampPrecision": string,
  "roundingMode": enum (RoundingMode),
  "collation": string,
  "defaultValueExpression": string,
  "rangeElementType": {
    object (FieldElementType)
  },
  "foreignTypeDefinition": string,
  "generatedColumn": {
    object (GeneratedColumn)
  }
}
```

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
<td><code>name</code></td>
<td><p><code>string</code></p>
<p>Required. The field name. The name must contain only letters (a-z, A-Z), numbers (0-9), or underscores (_), and must start with a letter or underscore. The maximum length is 300 characters.</p></td>
</tr>
<tr class="even">
<td><code>type</code></td>
<td><p><code>string</code></p>
<p>Required. The field data type. Possible values include:</p>
<ul>
<li>STRING</li>
<li>BYTES</li>
<li>INTEGER (or INT64)</li>
<li>FLOAT (or FLOAT64)</li>
<li>BOOLEAN (or BOOL)</li>
<li>TIMESTAMP</li>
<li>DATE</li>
<li>TIME</li>
<li>DATETIME</li>
<li>GEOGRAPHY</li>
<li>NUMERIC</li>
<li>BIGNUMERIC</li>
<li>JSON</li>
<li>RECORD (or STRUCT)</li>
<li>RANGE</li>
</ul>
<p>Use of RECORD/STRUCT indicates that the field contains a nested schema.</p></td>
</tr>
<tr class="odd">
<td><code>mode</code></td>
<td><p><code>string</code></p>
<p>Optional. The field mode. Possible values include NULLABLE, REQUIRED and REPEATED. The default value is NULLABLE.</p></td>
</tr>
<tr class="even">
<td><code>fields[]</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.TableFieldSchema"><code>TableFieldSchema</code></a><code> )</code></p>
<p>Optional. Describes the nested schema fields if the type property is set to RECORD.</p></td>
</tr>
<tr class="odd">
<td><code>description</code></td>
<td><p><code>string</code></p>
<p>Optional. The field description. The maximum length is 1,024 characters.</p></td>
</tr>
<tr class="even">
<td><code>policyTags</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.PolicyTagList"><code>PolicyTagList</code></a><code> )</code></p>
<p>Optional. The policy tags attached to this field, used for field-level access control. If not set, defaults to empty policy_tags.</p></td>
</tr>
<tr class="odd">
<td><code>dataGovernanceTagsInfo</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.DataGovernanceTagsInfo"><code>DataGovernanceTagsInfo</code></a><code> )</code></p>
<p>Optional. Specifies the data governance tags on this field. This field works with other column-level security fields as follows:</p>
<ul>
<li><strong>Precedence</strong> : If a data governance tag is attached to a column, it takes precedence over the policy tag attached to the column. However, if a data policy is attached to a column, it takes precedence over the data governance tag.</li>
<li><strong>Patching behavior</strong> : Describes how this field behaves during a <code>Table.patch</code> schema update:
<ul>
<li><strong>Unset</strong> : If the <code>data_governance_tags_info</code> field is omitted from the update request, the existing tags on the column are preserved.</li>
<li><strong>Empty Field</strong> : To clear data governance tags from a column, send the <code>data_governance_tags_info</code> field as an empty object. This removes all tags from the column.</li>
<li><strong>Updating tags</strong> : To replace an existing tag, send the field with the new tag.</li>
</ul></li>
</ul></td>
</tr>
<tr class="even">
<td><code>dataPolicies[]</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.DataPolicyOption"><code>DataPolicyOption</code></a><code> )</code></p>
<p>Optional. Data policies attached to this field, used for field-level access control.</p></td>
</tr>
<tr class="odd">
<td><code>dataPolicyList</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.DataPolicyList"><code>DataPolicyList</code></a><code> )</code></p>
<p>Optional. Specifies data policies attached to this field, used for field-level access control. When set, this will be the source of truth for data policy information.</p></td>
</tr>
<tr class="even">
<td><code>maxLength</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>int64</code></a><code> format)</code></p>
<p>Optional. Maximum length of values of this field for STRINGS or BYTES.</p>
<p>If max_length is not specified, no maximum length constraint is imposed on this field.</p>
<p>If type = "STRING", then max_length represents the maximum UTF-8 length of strings in this field.</p>
<p>If type = "BYTES", then max_length represents the maximum number of bytes in this field.</p>
<p>It is invalid to set this field if type ≠ "STRING" and ≠ "BYTES".</p></td>
</tr>
<tr class="odd">
<td><code>precision</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>int64</code></a><code> format)</code></p>
<p>Optional. Precision (maximum number of total digits in base 10) and scale (maximum number of digits in the fractional part in base 10) constraints for values of this field for NUMERIC or BIGNUMERIC.</p>
<p>It is invalid to set precision or scale if type ≠ "NUMERIC" and ≠ "BIGNUMERIC".</p>
<p>If precision and scale are not specified, no value range constraint is imposed on this field insofar as values are permitted by the type.</p>
<p>Values of this NUMERIC or BIGNUMERIC field must be in this range when:</p>
<ul>
<li>Precision ( <var translate="no"> P </var> ) and scale ( <var translate="no"> S </var> ) are specified: [-10 <sup><var translate="no"> P </var> - <var translate="no"> S </var></sup> + 10 <sup>- <var translate="no"> S </var></sup> , 10 <sup><var translate="no"> P </var> - <var translate="no"> S </var></sup> - 10 <sup>- <var translate="no"> S </var></sup> ]</li>
<li>Precision ( <var translate="no"> P </var> ) is specified but not scale (and thus scale is interpreted to be equal to zero): [-10 <sup><var translate="no"> P </var></sup> + 1, 10 <sup><var translate="no"> P </var></sup> - 1].</li>
</ul>
<p>Acceptable values for precision and scale if both are specified:</p>
<ul>
<li>If type = "NUMERIC": 1 ≤ precision - scale ≤ 29 and 0 ≤ scale ≤ 9.</li>
<li>If type = "BIGNUMERIC": 1 ≤ precision - scale ≤ 38 and 0 ≤ scale ≤ 38.</li>
</ul>
<p>Acceptable values for precision if only precision is specified but not scale (and thus scale is interpreted to be equal to zero):</p>
<ul>
<li>If type = "NUMERIC": 1 ≤ precision ≤ 29.</li>
<li>If type = "BIGNUMERIC": 1 ≤ precision ≤ 38.</li>
</ul>
<p>If scale is specified but not precision, then it is invalid.</p></td>
</tr>
<tr class="even">
<td><code>scale</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>int64</code></a><code> format)</code></p>
<p>Optional. See documentation for precision.</p></td>
</tr>
<tr class="odd">
<td><code>timestampPrecision</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>Int64Value</code></a><code> format)</code></p>
<p>Optional. Precision (maximum number of total digits in base 10) for seconds of TIMESTAMP type.</p>
<p>Possible values include: * 6 (Default, for TIMESTAMP type with microsecond precision) * 12 (For TIMESTAMP type with picosecond precision)</p></td>
</tr>
<tr class="even">
<td><code>roundingMode</code></td>
<td><p><code>enum ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_dataset_info#Output.Schema.RoundingMode"><code>RoundingMode</code></a><code> )</code></p>
<p>Optional. Specifies the rounding mode to be used when storing values of NUMERIC and BIGNUMERIC type.</p></td>
</tr>
<tr class="odd">
<td><code>collation</code></td>
<td><p><code>string</code></p>
<p>Optional. Field collation can be set only when the type of field is STRING. The following values are supported:</p>
<ul>
<li>'und:ci': undetermined locale, case insensitive.</li>
<li>'': empty string. Default to case-sensitive behavior.</li>
</ul></td>
</tr>
<tr class="even">
<td><code>defaultValueExpression</code></td>
<td><p><code>string</code></p>
<p>Optional. A SQL expression to specify the <a href="https://cloud.google.com/bigquery/docs/default-values">default value</a> for this field.</p></td>
</tr>
<tr class="odd">
<td><code>rangeElementType</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.FieldElementType"><code>FieldElementType</code></a><code> )</code></p>
<p>Optional. The subtype of the RANGE, if the type of this field is RANGE. If the type is RANGE, this field is required. Values for the field element type can be the following:</p>
<ul>
<li>DATE</li>
<li>DATETIME</li>
<li>TIMESTAMP</li>
</ul></td>
</tr>
<tr class="even">
<td><code>foreignTypeDefinition</code></td>
<td><p><code>string</code></p>
<p>Optional. Definition of the foreign data type. Only valid for top-level schema fields (not nested fields). If the type is FOREIGN, this field is required.</p></td>
</tr>
<tr class="odd">
<td><code>generatedColumn</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.GeneratedColumn"><code>GeneratedColumn</code></a><code> )</code></p>
<p>Optional. Definition of how values are generated for the field. Only valid for top-level schema fields (not nested fields).</p></td>
</tr>
</tbody>
</table>

### StringValue

**JSON representation**

```
{
  "value": string
}
```

| Fields  |                            |
|---------|----------------------------|
| `value` | `string` The string value. |

### PolicyTagList

**JSON representation**

```
{
  "names": [
    string
  ]
}
```

| Fields    |                                                                                                                                                            |
|-----------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `names[]` | `string` A list of policy tag resource names. For example, "projects/1/locations/eu/taxonomies/2/policyTags/3". At most 1 policy tag is currently allowed. |

### DataGovernanceTagsInfo

**JSON representation**

```
{
  "dataGovernanceTags": {
    string: string,
    ...
  }
}
```

| Fields               |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
|----------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `dataGovernanceTags` | `map (key: string, value: string)` Optional. The data governance tags added to this field are used for field-level access control. Only one data governance tag is currently supported on a field. Tag keys are globally unique. Tag key is expected to be in the namespaced format, for example "parent-id/pii" where parent-id is the ID of the parent organization or project resource for this tag key. Tag value is expected to be the short name, for example "sensitive". See [Tag definitions](https://cloud.google.com/iam/docs/tags-access-control#definitions) for more details. For example: "parent-id/pii": "sensitive", "myProject/cost_center": "sales" An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` . |

### DataGovernanceTagsEntry

**JSON representation**

```
{
  "key": string,
  "value": string
}
```

| Fields  |          |
|---------|----------|
| `key`   | `string` |
| `value` | `string` |

### DataPolicyOption

**JSON representation**

```
{

  // Union field _name can be only one of the following:
  "name": string
  // End of list of possible types for union field _name.
}
```

| Fields                                                          |                                                                                                                          |
|-----------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------|
| Union field `_name` . `_name` can be only one of the following: |                                                                                                                          |
| `name`                                                          | `string` Data policy resource name in the form of projects/project_id/locations/location_id/dataPolicies/data_policy_id. |
|                                                                 |                                                                                                                          |

### DataPolicyList

**JSON representation**

```
{
  "dataPolicies": [
    {
      object (DataPolicyOption)
    }
  ]
}
```

| Fields           |                                                                                                                                                                                                                                                |
|------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `dataPolicies[]` | `object ( `[`DataPolicyOption`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.DataPolicyOption)` )` Contains a list of data policy options. At most 9 data policies are allowed per field. |

### Int64Value

**JSON representation**

```
{
  "value": string
}
```

| Fields  |                                                                                                         |
|---------|---------------------------------------------------------------------------------------------------------|
| `value` | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` The int64 value. |

### FieldElementType

**JSON representation**

```
{
  "type": string
}
```

| Fields |                                                                                                     |
|--------|-----------------------------------------------------------------------------------------------------|
| `type` | `string` Required. The type of a field element. For more information, see `TableFieldSchema.type` . |

### GeneratedColumn

**JSON representation**

```
{

  // Union field _generated_mode can be only one of the following:
  "generatedMode": enum (GeneratedMode)
  // End of list of possible types for union field _generated_mode.

  // Union field definition can be only one of the following:
  "generatedExpressionInfo": {
    object (GeneratedExpressionInfo)
  }
  // End of list of possible types for union field definition.
}
```

| Fields                                                                              |                                                                                                                                                                                                                                 |
|-------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `_generated_mode` . `_generated_mode` can be only one of the following: |                                                                                                                                                                                                                                 |
| `generatedMode`                                                                     | `enum ( `[`GeneratedMode`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.GeneratedMode)` )` Optional. Dictates when system generated values are used to populate the field. |
|                                                                                     |                                                                                                                                                                                                                                 |
| Union field `definition` . `definition` can be only one of the following:           |                                                                                                                                                                                                                                 |
| `generatedExpressionInfo`                                                           | `object ( `[`GeneratedExpressionInfo`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.GeneratedExpressionInfo)` )` Definition of the expression used to generate the field.  |
|                                                                                     |                                                                                                                                                                                                                                 |

### GeneratedExpressionInfo

**JSON representation**

```
{

  // Union field _generation_expression can be only one of the following:
  "generationExpression": string
  // End of list of possible types for union field _generation_expression.

  // Union field _asynchronous can be only one of the following:
  "asynchronous": boolean
  // End of list of possible types for union field _asynchronous.

  // Union field _stored can be only one of the following:
  "stored": boolean
  // End of list of possible types for union field _stored.
}
```

| Fields                                                                                            |                                                                                               |
|---------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------|
| Union field `_generation_expression` . `_generation_expression` can be only one of the following: |                                                                                               |
| `generationExpression`                                                                            | `string` Optional. The generation expression (e.g. AI.EMBED(...)) used to generate the field. |
|                                                                                                   |                                                                                               |
| Union field `_asynchronous` . `_asynchronous` can be only one of the following:                   |                                                                                               |
| `asynchronous`                                                                                    | `boolean` Optional. Whether the column generation is done asynchronously.                     |
|                                                                                                   |                                                                                               |
| Union field `_stored` . `_stored` can be only one of the following:                               |                                                                                               |
| `stored`                                                                                          | `boolean` Optional. Whether the generated column is stored in the table.                      |
|                                                                                                   |                                                                                               |

### ForeignTypeInfo

**JSON representation**

```
{
  "typeSystem": enum (TypeSystem)
}
```

| Fields       |                                                                                                                                                                                                               |
|--------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `typeSystem` | `enum ( `[`TypeSystem`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.TypeSystem)` )` Required. Specifies the system which defines the foreign data type. |

### Int32Value

**JSON representation**

```
{
  "value": integer
}
```

| Fields  |                            |
|---------|----------------------------|
| `value` | `integer` The int32 value. |

### BoolValue

**JSON representation**

```
{
  "value": boolean
}
```

| Fields  |                           |
|---------|---------------------------|
| `value` | `boolean` The bool value. |

### CsvOptions

**JSON representation**

```
{
  "fieldDelimiter": string,
  "skipLeadingRows": string,
  "quote": string,
  "allowQuotedNewlines": boolean,
  "allowJaggedRows": boolean,
  "encoding": string,
  "preserveAsciiControlCharacters": boolean,
  "nullMarker": string,
  "nullMarkers": [
    string
  ],
  "sourceColumnMatch": string
}
```

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
<td><code>fieldDelimiter</code></td>
<td><p><code>string</code></p>
<p>Optional. The separator character for fields in a CSV file. The separator is interpreted as a single byte. For files encoded in ISO-8859-1, any single character can be used as a separator. For files encoded in UTF-8, characters represented in decimal range 1-127 (U+0001-U+007F) can be used without any modification. UTF-8 characters encoded with multiple bytes (i.e. U+0080 and above) will have only the first byte used for separating fields. The remaining bytes will be treated as a part of the field. BigQuery also supports the escape sequence "\t" (U+0009) to specify a tab separator. The default value is comma (",", U+002C).</p></td>
</tr>
<tr class="even">
<td><code>skipLeadingRows</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>Int64Value</code></a><code> format)</code></p>
<p>Optional. The number of rows at the top of a CSV file that BigQuery will skip when reading the data. The default value is 0. This property is useful if you have header rows in the file that should be skipped. When autodetect is on, the behavior is the following:</p>
<ul>
<li>skipLeadingRows unspecified - Autodetect tries to detect headers in the first row. If they are not detected, the row is read as data. Otherwise data is read starting from the second row.</li>
<li>skipLeadingRows is 0 - Instructs autodetect that there are no headers and data should be read starting from the first row.</li>
<li>skipLeadingRows = N &gt; 0 - Autodetect skips N-1 rows and tries to detect headers in row N. If headers are not detected, row N is just skipped. Otherwise row N is used to extract column names for the detected schema.</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>quote</code></td>
<td><p><code>string</code></p>
<p>Optional. The value that is used to quote data sections in a CSV file. BigQuery converts the string to ISO-8859-1 encoding, and then uses the first byte of the encoded string to split the data in its raw, binary state. The default value is a double-quote ("). If your data does not contain quoted sections, set the property value to an empty string. If your data contains quoted newline characters, you must also set the allowQuotedNewlines property to true. To include the specific quote character within a quoted value, precede it with an additional matching quote character. For example, if you want to escape the default character ' " ', use ' "" '.</p></td>
</tr>
<tr class="even">
<td><code>allowQuotedNewlines</code></td>
<td><p><code>boolean</code></p>
<p>Optional. Indicates if BigQuery should allow quoted data sections that contain newline characters in a CSV file. The default value is false.</p></td>
</tr>
<tr class="odd">
<td><code>allowJaggedRows</code></td>
<td><p><code>boolean</code></p>
<p>Optional. Indicates if BigQuery should accept rows that are missing trailing optional columns. If true, BigQuery treats missing trailing columns as null values. If false, records with missing trailing columns are treated as bad records, and if there are too many bad records, an invalid error is returned in the job result. The default value is false.</p></td>
</tr>
<tr class="even">
<td><code>encoding</code></td>
<td><p><code>string</code></p>
<p>Optional. The character encoding of the data. The supported values are UTF-8, ISO-8859-1, UTF-16BE, UTF-16LE, UTF-32BE, and UTF-32LE. The default value is UTF-8. BigQuery decodes the data after the raw, binary data has been split using the values of the quote and fieldDelimiter properties.</p></td>
</tr>
<tr class="odd">
<td><code>preserveAsciiControlCharacters</code></td>
<td><p><code>boolean</code></p>
<p>Optional. Indicates if the embedded ASCII control characters (the first 32 characters in the ASCII-table, from '\x00' to '\x1F') are preserved.</p></td>
</tr>
<tr class="even">
<td><code>nullMarker</code></td>
<td><p><code>string</code></p>
<p>Optional. Specifies a string that represents a null value in a CSV file. For example, if you specify "\N", BigQuery interprets "\N" as a null value when querying a CSV file. The default value is the empty string. If you set this property to a custom value, BigQuery throws an error if an empty string is present for all data types except for STRING and BYTE. For STRING and BYTE columns, BigQuery interprets the empty string as an empty value.</p></td>
</tr>
<tr class="odd">
<td><code>nullMarkers[]</code></td>
<td><p><code>string</code></p>
<p>Optional. A list of strings represented as SQL NULL value in a CSV file.</p>
<p>null_marker and null_markers can't be set at the same time. If null_marker is set, null_markers has to be not set. If null_markers is set, null_marker has to be not set. If both null_marker and null_markers are set at the same time, a user error would be thrown. Any strings listed in null_markers, including empty string would be interpreted as SQL NULL. This applies to all column types.</p></td>
</tr>
<tr class="even">
<td><code>sourceColumnMatch</code></td>
<td><p><code>string</code></p>
<p>Optional. Controls the strategy used to match loaded columns to the schema. If not set, a sensible default is chosen based on how the schema is provided. If autodetect is used, then columns are matched by name. Otherwise, columns are matched by position. This is done to keep the behavior backward-compatible. Acceptable values are: POSITION - matches by position. This assumes that the columns are ordered the same way as the schema. NAME - matches by name. This reads the header row as column names and reorders columns to match the field names in the schema.</p></td>
</tr>
</tbody>
</table>

### JsonOptions

**JSON representation**

```
{
  "encoding": string
}
```

| Fields     |                                                                                                                                                                |
|------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `encoding` | `string` Optional. The character encoding of the data. The supported values are UTF-8, UTF-16BE, UTF-16LE, UTF-32BE, and UTF-32LE. The default value is UTF-8. |

### BigtableOptions

**JSON representation**

```
{
  "columnFamilies": [
    {
      object (BigtableColumnFamily)
    }
  ],
  "ignoreUnspecifiedColumnFamilies": boolean,
  "readRowkeyAsString": boolean,
  "outputColumnFamiliesAsJson": boolean
}
```

| Fields                            |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
|-----------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `columnFamilies[]`                | `object ( `[`BigtableColumnFamily`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.BigtableColumnFamily)` )` Optional. List of column families to expose in the table schema along with their types. This list restricts the column families that can be referenced in queries and specifies their value types. You can use this list to do type conversions - see the 'type' field for more details. If you leave this list empty, all column families are present in the table schema and their values are read as BYTES. During a query only the column families referenced in that query are read from Bigtable. |
| `ignoreUnspecifiedColumnFamilies` | `boolean` Optional. If field is true, then the column families that are not specified in columnFamilies list are not exposed in the table schema. Otherwise, they are read with BYTES type values. The default value is false.                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| `readRowkeyAsString`              | `boolean` Optional. If field is true, then the rowkey column families will be read and converted to string. Otherwise they are read with BYTES type values and users need to manually cast them with CAST if necessary. The default value is false.                                                                                                                                                                                                                                                                                                                                                                                                                     |
| `outputColumnFamiliesAsJson`      | `boolean` Optional. If field is true, then each column family will be read as a single JSON column. Otherwise they are read as a repeated cell structure containing timestamp/value tuples. The default value is false.                                                                                                                                                                                                                                                                                                                                                                                                                                                 |

### BigtableColumnFamily

**JSON representation**

```
{
  "familyId": string,
  "type": string,
  "encoding": string,
  "columns": [
    {
      object (BigtableColumn)
    }
  ],
  "onlyReadLatest": boolean,
  "protoConfig": {
    object (BigtableProtoConfig)
  }
}
```

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
<td><code>familyId</code></td>
<td><p><code>string</code></p>
<p>Identifier of the column family.</p></td>
</tr>
<tr class="even">
<td><code>type</code></td>
<td><p><code>string</code></p>
<p>Optional. The type to convert the value in cells of this column family. The values are expected to be encoded using HBase Bytes.toBytes function when using the BINARY encoding value. Following BigQuery types are allowed (case-sensitive):</p>
<ul>
<li>BYTES</li>
<li>STRING</li>
<li>INTEGER</li>
<li>FLOAT</li>
<li>BOOLEAN</li>
<li>JSON</li>
</ul>
<p>Default type is BYTES. This can be overridden for a specific column by listing that column in 'columns' and specifying a type for it.</p></td>
</tr>
<tr class="odd">
<td><code>encoding</code></td>
<td><p><code>string</code></p>
<p>Optional. The encoding of the values when the type is not STRING. Acceptable encoding values are: TEXT - indicates values are alphanumeric text strings. BINARY - indicates values are encoded using HBase Bytes.toBytes family of functions. PROTO_BINARY - indicates values are encoded using serialized proto messages. This can only be used in combination with JSON type. This can be overridden for a specific column by listing that column in 'columns' and specifying an encoding for it.</p></td>
</tr>
<tr class="even">
<td><code>columns[]</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.BigtableColumn"><code>BigtableColumn</code></a><code> )</code></p>
<p>Optional. Lists of columns that should be exposed as individual fields as opposed to a list of (column name, value) pairs. All columns whose qualifier matches a qualifier in this list can be accessed as <code>&lt;family field name&gt;.&lt;column field name&gt;</code> . Other columns can be accessed as a list through the <code>&lt;family field name&gt;.Column</code> field.</p></td>
</tr>
<tr class="odd">
<td><code>onlyReadLatest</code></td>
<td><p><code>boolean</code></p>
<p>Optional. If this is set only the latest version of value are exposed for all columns in this column family. This can be overridden for a specific column by listing that column in 'columns' and specifying a different setting for that column.</p></td>
</tr>
<tr class="even">
<td><code>protoConfig</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.BigtableProtoConfig"><code>BigtableProtoConfig</code></a><code> )</code></p>
<p>Optional. Protobuf-specific configurations, only takes effect when the encoding is PROTO_BINARY.</p></td>
</tr>
</tbody>
</table>

### BigtableColumn

**JSON representation**

```
{
  "qualifierEncoded": string,
  "qualifierString": string,
  "fieldName": string,
  "type": string,
  "encoding": string,
  "onlyReadLatest": boolean,
  "protoConfig": {
    object (BigtableProtoConfig)
  }
}
```

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
<td><code>qualifierEncoded</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>BytesValue</code></a><code> format)</code></p>
<p>[Required] Qualifier of the column. Columns in the parent column family that has this exact qualifier are exposed as <code>&lt;family field name&gt;.&lt;column field name&gt;</code> field. If the qualifier is valid UTF-8 string, it can be specified in the qualifier_string field. Otherwise, a base-64 encoded value must be set to qualifier_encoded. The column field name is the same as the column qualifier. However, if the qualifier is not a valid BigQuery field identifier i.e. does not match [a-zA-Z][a-zA-Z0-9_]*, a valid identifier must be provided as field_name.</p></td>
</tr>
<tr class="even">
<td><code>qualifierString</code></td>
<td><p><code>string</code></p>
<p>Qualifier string.</p></td>
</tr>
<tr class="odd">
<td><code>fieldName</code></td>
<td><p><code>string</code></p>
<p>Optional. If the qualifier is not a valid BigQuery field identifier i.e. does not match [a-zA-Z][a-zA-Z0-9_]*, a valid identifier must be provided as the column field name and is used as field name in queries.</p></td>
</tr>
<tr class="even">
<td><code>type</code></td>
<td><p><code>string</code></p>
<p>Optional. The type to convert the value in cells of this column. The values are expected to be encoded using HBase Bytes.toBytes function when using the BINARY encoding value. Following BigQuery types are allowed (case-sensitive):</p>
<ul>
<li>BYTES</li>
<li>STRING</li>
<li>INTEGER</li>
<li>FLOAT</li>
<li>BOOLEAN</li>
<li>JSON</li>
</ul>
<p>Default type is BYTES. 'type' can also be set at the column family level. However, the setting at this level takes precedence if 'type' is set at both levels.</p></td>
</tr>
<tr class="odd">
<td><code>encoding</code></td>
<td><p><code>string</code></p>
<p>Optional. The encoding of the values when the type is not STRING. Acceptable encoding values are: TEXT - indicates values are alphanumeric text strings. BINARY - indicates values are encoded using HBase Bytes.toBytes family of functions. PROTO_BINARY - indicates values are encoded using serialized proto messages. This can only be used in combination with JSON type. 'encoding' can also be set at the column family level. However, the setting at this level takes precedence if 'encoding' is set at both levels.</p></td>
</tr>
<tr class="even">
<td><code>onlyReadLatest</code></td>
<td><p><code>boolean</code></p>
<p>Optional. If this is set, only the latest version of value in this column are exposed. 'onlyReadLatest' can also be set at the column family level. However, the setting at this level takes precedence if 'onlyReadLatest' is set at both levels.</p></td>
</tr>
<tr class="odd">
<td><code>protoConfig</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.BigtableProtoConfig"><code>BigtableProtoConfig</code></a><code> )</code></p>
<p>Optional. Protobuf-specific configurations, only takes effect when the encoding is PROTO_BINARY.</p></td>
</tr>
</tbody>
</table>

### BytesValue

**JSON representation**

```
{
  "value": string
}
```

| Fields  |                                                                                                                                  |
|---------|----------------------------------------------------------------------------------------------------------------------------------|
| `value` | `string ( `[`bytes`](https://developers.google.com/discovery/v1/type-format)` format)` The bytes value. A base64-encoded string. |

### BigtableProtoConfig

**JSON representation**

```
{
  "schemaBundleId": string,
  "protoMessageName": string
}
```

| Fields             |                                                                                                                                                                                                                                                                                                                                                                                      |
|--------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `schemaBundleId`   | `string` Optional. The ID of the Bigtable SchemaBundle resource associated with this protobuf. The ID should be referred to within the parent table, e.g., `foo` rather than `projects/{project}/instances/{instance}/tables/{table}/schemaBundles/foo` . See [more details on Bigtable SchemaBundles](https://docs.cloud.google.com/bigtable/docs/create-manage-protobuf-schemas) . |
| `protoMessageName` | `string` Optional. The fully qualified proto message name of the protobuf. In the format of "foo.bar.Message".                                                                                                                                                                                                                                                                       |

### GoogleSheetsOptions

**JSON representation**

```
{
  "skipLeadingRows": string,
  "range": string
}
```

| Fields            |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
|-------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `skipLeadingRows` | `string ( `[`Int64Value`](https://developers.google.com/discovery/v1/type-format)` format)` Optional. The number of rows at the top of a sheet that BigQuery will skip when reading the data. The default value is 0. This property is useful if you have header rows that should be skipped. When autodetect is on, the behavior is the following: \* skipLeadingRows unspecified - Autodetect tries to detect headers in the first row. If they are not detected, the row is read as data. Otherwise data is read starting from the second row. \* skipLeadingRows is 0 - Instructs autodetect that there are no headers and data should be read starting from the first row. \* skipLeadingRows = N \> 0 - Autodetect skips N-1 rows and tries to detect headers in row N. If headers are not detected, row N is just skipped. Otherwise row N is used to extract column names for the detected schema. |
| `range`           | `string` Optional. Range of a sheet to query from. Only used when non-empty. Typical format: sheet_name!top_left_cell_id:bottom_right_cell_id For example: sheet1!A1:B20                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |

### HivePartitioningOptions

**JSON representation**

```
{
  "mode": string,
  "sourceUriPrefix": string,
  "requirePartitionFilter": boolean,
  "fields": [
    string
  ]
}
```

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
<td><code>mode</code></td>
<td><p><code>string</code></p>
<p>Optional. When set, what mode of hive partitioning to use when reading data. The following modes are supported:</p>
<ul>
<li><p>AUTO: automatically infer partition key name(s) and type(s).</p></li>
<li><p>STRINGS: automatically infer partition key name(s). All types are strings.</p></li>
<li><p>CUSTOM: partition key schema is encoded in the source URI prefix.</p></li>
</ul>
<p>Not all storage formats support hive partitioning. Requesting hive partitioning on an unsupported format will lead to an error. Currently supported formats are: JSON, CSV, ORC, Avro and Parquet.</p></td>
</tr>
<tr class="even">
<td><code>sourceUriPrefix</code></td>
<td><p><code>string</code></p>
<p>Optional. When hive partition detection is requested, a common prefix for all source uris must be required. The prefix must end immediately before the partition key encoding begins. For example, consider files following this data layout:</p>
<p>gs://bucket/path_to_table/dt=2019-06-01/country=USA/id=7/file.avro</p>
<p>gs://bucket/path_to_table/dt=2019-05-31/country=CA/id=3/file.avro</p>
<p>When hive partitioning is requested with either AUTO or STRINGS detection, the common prefix can be either of gs://bucket/path_to_table or gs://bucket/path_to_table/.</p>
<p>CUSTOM detection requires encoding the partitioning schema immediately after the common prefix. For CUSTOM, any of</p>
<ul>
<li><p>gs://bucket/path_to_table/{dt:DATE}/{country:STRING}/{id:INTEGER}</p></li>
<li><p>gs://bucket/path_to_table/{dt:STRING}/{country:STRING}/{id:INTEGER}</p></li>
<li><p>gs://bucket/path_to_table/{dt:DATE}/{country:STRING}/{id:STRING}</p></li>
</ul>
<p>would all be valid source URI prefixes.</p></td>
</tr>
<tr class="odd">
<td><code>requirePartitionFilter</code></td>
<td><p><code>boolean</code></p>
<p>Optional. If set to true, queries over this table require a partition filter that can be used for partition elimination to be specified.</p>
<p>Note that this field should only be true when creating a permanent external table or querying a temporary external table.</p>
<p>Hive-partitioned loads with require_partition_filter explicitly set to true will fail.</p></td>
</tr>
<tr class="even">
<td><code>fields[]</code></td>
<td><p><code>string</code></p>
<p>Output only. For permanent external tables, this field is populated with the hive partition keys in the order they were inferred. The types of the partition keys can be deduced by checking the table schema (which will include the partition keys). Not every API will populate this field in the output. For example, Tables.Get will populate it, but Tables.List will not contain this field.</p></td>
</tr>
</tbody>
</table>

### AvroOptions

**JSON representation**

```
{
  "useAvroLogicalTypes": boolean
}
```

| Fields                |                                                                                                                                                                                                                            |
|-----------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `useAvroLogicalTypes` | `boolean` Optional. If sourceFormat is set to "AVRO", indicates whether to interpret logical types as the corresponding BigQuery data type (for example, TIMESTAMP), instead of using the raw type (for example, INTEGER). |

### ParquetOptions

**JSON representation**

```
{
  "enumAsString": boolean,
  "enableListInference": boolean,
  "mapTargetType": enum (MapTargetType)
}
```

| Fields                |                                                                                                                                                                                                                |
|-----------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `enumAsString`        | `boolean` Optional. Indicates whether to infer Parquet ENUM logical type as STRING instead of BYTES by default.                                                                                                |
| `enableListInference` | `boolean` Optional. Indicates whether to use schema inference specifically for Parquet LIST logical type.                                                                                                      |
| `mapTargetType`       | `enum ( `[`MapTargetType`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.MapTargetType)` )` Optional. Indicates how to represent a Parquet map if present. |

### UserDefinedFunctionResource

**JSON representation**

```
{
  "resourceUri": string,
  "inlineCode": string
}
```

| Fields        |                                                                                                                                                                                                       |
|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `resourceUri` | `string` \[Pick one\] A code resource to load from a Google Cloud Storage URI (gs://bucket/path).                                                                                                     |
| `inlineCode`  | `string` \[Pick one\] An inline resource that contains code for a user-defined function (UDF). Providing a inline code resource is equivalent to providing a URI for a file containing the same code. |

### DatasetReference

**JSON representation**

```
{
  "datasetId": string,
  "projectId": string
}
```

| Fields      |                                                                                                                                                                                                     |
|-------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `datasetId` | `string` Required. A unique ID for this dataset, without the project name. The ID must contain only letters (a-z, A-Z), numbers (0-9), or underscores (\_). The maximum length is 1,024 characters. |
| `projectId` | `string` Optional. The ID of the project containing this dataset.                                                                                                                                   |

### QueryParameter

**JSON representation**

```
{
  "name": string,
  "parameterType": {
    object (QueryParameterType)
  },
  "parameterValue": {
    object (QueryParameterValue)
  }
}
```

| Fields           |                                                                                                                                                                                                  |
|------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`           | `string` Optional. If unset, this is a positional parameter. Otherwise, should be unique within a query.                                                                                         |
| `parameterType`  | `object ( `[`QueryParameterType`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.QueryParameterType)` )` Required. The type of this parameter.    |
| `parameterValue` | `object ( `[`QueryParameterValue`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.QueryParameterValue)` )` Required. The value of this parameter. |

### QueryParameterType

**JSON representation**

```
{
  "type": string,
  "arrayType": {
    object (QueryParameterType)
  },
  "structTypes": [
    {
      object (QueryParameterStructType)
    }
  ],
  "rangeElementType": {
    object (QueryParameterType)
  },

  // Union field _timestamp_precision can be only one of the following:
  "timestampPrecision": string
  // End of list of possible types for union field _timestamp_precision.
}
```

| Fields                                                                                        |                                                                                                                                                                                                                                                                                                                                   |
|-----------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `type`                                                                                        | `string` Required. The top level type of this field.                                                                                                                                                                                                                                                                              |
| `arrayType`                                                                                   | `object ( `[`QueryParameterType`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.QueryParameterType)` )` Optional. The type of the array's elements, if this is an array.                                                                                                          |
| `structTypes[]`                                                                               | `object ( `[`QueryParameterStructType`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.QueryParameterStructType)` )` Optional. The types of the fields of this struct, in order, if this is a struct.                                                                              |
| `rangeElementType`                                                                            | `object ( `[`QueryParameterType`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.QueryParameterType)` )` Optional. The element type of the range, if this is a range.                                                                                                              |
| Union field `_timestamp_precision` . `_timestamp_precision` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                   |
| `timestampPrecision`                                                                          | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Optional. Precision (maximum number of total digits in base 10) for seconds of TIMESTAMP type. Possible values include: \* 6 (Default, for TIMESTAMP type with microsecond precision) \* 12 (For TIMESTAMP type with picosecond precision) |
|                                                                                               |                                                                                                                                                                                                                                                                                                                                   |

### QueryParameterStructType

**JSON representation**

```
{
  "name": string,
  "type": {
    object (QueryParameterType)
  },
  "description": string
}
```

| Fields        |                                                                                                                                                                                           |
|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`        | `string` Optional. The name of this field.                                                                                                                                                |
| `type`        | `object ( `[`QueryParameterType`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.QueryParameterType)` )` Required. The type of this field. |
| `description` | `string` Optional. Human-oriented description of the field.                                                                                                                               |

### QueryParameterValue

**JSON representation**

```
{
  "value": string,
  "arrayValues": [
    {
      object (QueryParameterValue)
    }
  ],
  "structValues": {
    string: {
      object (QueryParameterValue)
    },
    ...
  },
  "rangeValue": {
    object (RangeValue)
  }
}
```

| Fields          |                                                                                                                                                                                                                                                                                                                                    |
|-----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `value`         | `string` Optional. The value of this value, if a simple scalar type.                                                                                                                                                                                                                                                               |
| `arrayValues[]` | `object ( `[`QueryParameterValue`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.QueryParameterValue)` )` Optional. The array values, if this is an array type.                                                                                                                    |
| `structValues`  | `map (key: string, value: object ( `[`QueryParameterValue`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.QueryParameterValue)` ))` The struct field values. An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` . |
| `rangeValue`    | `object ( `[`RangeValue`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.RangeValue)` )` Optional. The range value, if this is a range type.                                                                                                                                        |

### StructValuesEntry

**JSON representation**

```
{
  "key": string,
  "value": {
    object (QueryParameterValue)
  }
}
```

| Fields  |                                                                                                                                                           |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|
| `key`   | `string`                                                                                                                                                  |
| `value` | `object ( `[`QueryParameterValue`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.QueryParameterValue)` )` |

### RangeValue

**JSON representation**

```
{
  "start": {
    object (QueryParameterValue)
  },
  "end": {
    object (QueryParameterValue)
  }
}
```

| Fields  |                                                                                                                                                                                                                                                  |
|---------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `start` | `object ( `[`QueryParameterValue`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.QueryParameterValue)` )` Optional. The start value of the range. A missing value represents an unbounded start. |
| `end`   | `object ( `[`QueryParameterValue`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.QueryParameterValue)` )` Optional. The end value of the range. A missing value represents an unbounded end.     |

### SystemVariables

**JSON representation**

```
{
  "types": {
    string: {
      object (StandardSqlDataType)
    },
    ...
  },
  "values": {
    object
  }
}
```

| Fields   |                                                                                                                                                                                                                                                                                                                                                            |
|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `types`  | `map (key: string, value: object ( `[`StandardSqlDataType`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.StandardSqlDataType)` ))` Output only. Data type for each system variable. An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` . |
| `values` | `object ( `[`Struct`](https://protobuf.dev/reference/protobuf/google.protobuf/#struct)` format)` Output only. Value for each system variable.                                                                                                                                                                                                              |

### TypesEntry

**JSON representation**

```
{
  "key": string,
  "value": {
    object (StandardSqlDataType)
  }
}
```

| Fields  |                                                                                                                                                           |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|
| `key`   | `string`                                                                                                                                                  |
| `value` | `object ( `[`StandardSqlDataType`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.StandardSqlDataType)` )` |

### StandardSqlDataType

**JSON representation**

```
{
  "typeKind": enum (TypeKind),

  // Union field sub_type can be only one of the following:
  "arrayElementType": {
    object (StandardSqlDataType)
  },
  "structType": {
    object (StandardSqlStructType)
  },
  "rangeElementType": {
    object (StandardSqlDataType)
  }
  // End of list of possible types for union field sub_type.
}
```

| Fields                                                                                                             |                                                                                                                                                                                                                                                |
|--------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `typeKind`                                                                                                         | `enum ( `[`TypeKind`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.TypeKind)` )` Required. The top level type of this field. Can be any GoogleSQL data type (e.g., "INT64", "DATE", "ARRAY"). |
| Union field `sub_type` . For complex types, the sub type information. `sub_type` can be only one of the following: |                                                                                                                                                                                                                                                |
| `arrayElementType`                                                                                                 | `object ( `[`StandardSqlDataType`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.StandardSqlDataType)` )` The type of the array's elements, if type_kind = "ARRAY".                            |
| `structType`                                                                                                       | `object ( `[`StandardSqlStructType`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.StandardSqlStructType)` )` The fields of this struct, in order, if type_kind = "STRUCT".                    |
| `rangeElementType`                                                                                                 | `object ( `[`StandardSqlDataType`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.StandardSqlDataType)` )` The type of the range's elements, if type_kind = "RANGE".                            |
|                                                                                                                    |                                                                                                                                                                                                                                                |

### StandardSqlStructType

**JSON representation**

```
{
  "fields": [
    {
      object (StandardSqlField)
    }
  ]
}
```

| Fields     |                                                                                                                                                                               |
|------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `fields[]` | `object ( `[`StandardSqlField`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.StandardSqlField)` )` Fields within the struct. |

### StandardSqlField

**JSON representation**

```
{
  "name": string,
  "type": {
    object (StandardSqlDataType)
  }
}
```

| Fields |                                                                                                                                                                                                                                                                                                                                                                   |
|--------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name` | `string` Optional. The name of this field. Can be absent for struct fields.                                                                                                                                                                                                                                                                                       |
| `type` | `object ( `[`StandardSqlDataType`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.StandardSqlDataType)` )` Optional. The type of this parameter. Absent if not explicitly specified (e.g., CREATE FUNCTION statement can omit the return type; in this case the output parameter does not have this "type" field). |

### Struct

**JSON representation**

```
{
  "fields": {
    string: value,
    ...
  }
}
```

| Fields   |                                                                                                                                                                                                                                                                                          |
|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `fields` | `map (key: string, value: value ( `[`Value`](https://protobuf.dev/reference/protobuf/google.protobuf/#value)` format))` Unordered map of dynamically typed values. An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` . |

### FieldsEntry

**JSON representation**

```
{
  "key": string,
  "value": value
}
```

| Fields  |                                                                                               |
|---------|-----------------------------------------------------------------------------------------------|
| `key`   | `string`                                                                                      |
| `value` | `value ( `[`Value`](https://protobuf.dev/reference/protobuf/google.protobuf/#value)` format)` |

### Value

**JSON representation**

```
{

  // Union field kind can be only one of the following:
  "nullValue": null,
  "numberValue": number,
  "stringValue": string,
  "boolValue": boolean,
  "structValue": {
    object
  },
  "listValue": array
  // End of list of possible types for union field kind.
}
```

| Fields                                                                           |                                                                                                                                                                                                                                                |
|----------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `kind` . The kind of value. `kind` can be only one of the following: |                                                                                                                                                                                                                                                |
| `nullValue`                                                                      | `null` Represents a JSON `null` .                                                                                                                                                                                                              |
| `numberValue`                                                                    | `number` Represents a JSON number. Must not be `NaN` , `Infinity` or `-Infinity` , since those are not supported in JSON. This also cannot represent large Int64 values, since JSON format generally does not support them in its number type. |
| `stringValue`                                                                    | `string` Represents a JSON string.                                                                                                                                                                                                             |
| `boolValue`                                                                      | `boolean` Represents a JSON boolean ( `true` or `false` literal in JSON).                                                                                                                                                                      |
| `structValue`                                                                    | `object ( `[`Struct`](https://protobuf.dev/reference/protobuf/google.protobuf/#struct)` format)` Represents a JSON object.                                                                                                                     |
| `listValue`                                                                      | `array ( `[`ListValue`](https://protobuf.dev/reference/protobuf/google.protobuf/#list-value)` format)` Represents a JSON array.                                                                                                                |
|                                                                                  |                                                                                                                                                                                                                                                |

### ListValue

**JSON representation**

```
{
  "values": [
    value
  ]
}
```

| Fields     |                                                                                                                                           |
|------------|-------------------------------------------------------------------------------------------------------------------------------------------|
| `values[]` | `value ( `[`Value`](https://protobuf.dev/reference/protobuf/google.protobuf/#value)` format)` Repeated field of dynamically typed values. |

### TimePartitioning

**JSON representation**

```
{
  "type": string,
  "expirationMs": string,
  "field": string,
  "requirePartitionFilter": boolean
}
```

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
<td><code>type</code></td>
<td><p><code>string</code></p>
<p>Required. The supported types are DAY, HOUR, MONTH, and YEAR, which will generate one partition per day, hour, month, and year, respectively.</p></td>
</tr>
<tr class="even">
<td><code>expirationMs</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>Int64Value</code></a><code> format)</code></p>
<p>Optional. Number of milliseconds for which to keep the storage for a partition. A wrapper is used here because 0 is an invalid value.</p></td>
</tr>
<tr class="odd">
<td><code>field</code></td>
<td><p><code>string</code></p>
<p>Optional. If not set, the table is partitioned by pseudo column '_PARTITIONTIME'; if set, the table is partitioned by this field. The field must be a top-level TIMESTAMP or DATE field. Its mode must be NULLABLE or REQUIRED. A wrapper is used here because an empty string is an invalid value.</p></td>
</tr>
<tr class="even">
<td><code>requirePartitionFilter </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>boolean</code></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>If set to true, queries over this table require a partition filter that can be used for partition elimination to be specified. This field is deprecated; please set the field with the same name on the table itself instead. This field needs a wrapper because we want to output the default value, false, if the user explicitly set it.</p></td>
</tr>
</tbody>
</table>

### RangePartitioning

**JSON representation**

```
{
  "field": string,
  "range": {
    object (Range)
  }
}
```

| Fields  |                                                                                                                                                                              |
|---------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `field` | `string` Required. The name of the column to partition the table on. It must be a top-level, INT64 column whose mode is NULLABLE or REQUIRED.                                |
| `range` | `object ( `[`Range`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.Range)` )` Defines the ranges for range partitioning. |

### Range

**JSON representation**

```
{
  "start": string,
  "end": string,
  "interval": string
}
```

| Fields     |                                                                                                                      |
|------------|----------------------------------------------------------------------------------------------------------------------|
| `start`    | `string` Required. The start of range partitioning, inclusive. This field is an INT64 value represented as a string. |
| `end`      | `string` Required. The end of range partitioning, exclusive. This field is an INT64 value represented as a string.   |
| `interval` | `string` Required. The width of each interval. This field is an INT64 value represented as a string.                 |

### Clustering

**JSON representation**

```
{
  "fields": [
    string
  ]
}
```

| Fields     |                                                                                                                                                                                                                                                                                                                                                                                           |
|------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `fields[]` | `string` One or more fields on which data should be clustered. Only top-level, non-repeated, simple-type fields are supported. The ordering of the clustering fields should be prioritized from most to least important for filtering purposes. For additional information, see [Introduction to clustered tables](https://cloud.google.com/bigquery/docs/clustered-tables#limitations) . |

### EncryptionConfiguration

**JSON representation**

```
{
  "kmsKeyName": string
}
```

| Fields       |                                                                                                                                                                                                                      |
|--------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `kmsKeyName` | `string` Optional. Describes the Cloud KMS encryption key that will be used to protect destination BigQuery table. The BigQuery Service Account associated with your project requires access to this encryption key. |

### ScriptOptions

**JSON representation**

```
{
  "statementTimeoutMs": string,
  "statementByteBudget": string,
  "keyResultStatement": enum (KeyResultStatementKind)
}
```

| Fields                |                                                                                                                                                                                                                                                                                                                       |
|-----------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `statementTimeoutMs`  | `string ( `[`Int64Value`](https://developers.google.com/discovery/v1/type-format)` format)` Timeout period for each statement in a script.                                                                                                                                                                            |
| `statementByteBudget` | `string ( `[`Int64Value`](https://developers.google.com/discovery/v1/type-format)` format)` Limit on the number of bytes billed per statement. Exceeding this budget results in an error.                                                                                                                             |
| `keyResultStatement`  | `enum ( `[`KeyResultStatementKind`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.KeyResultStatementKind)` )` Determines which statement in the script represents the "key result", used to populate the schema and query results of the script job. Default is LAST. |

### ConnectionProperty

**JSON representation**

```
{
  "key": string,
  "value": string
}
```

| Fields  |                                            |
|---------|--------------------------------------------|
| `key`   | `string` The key of the property to set.   |
| `value` | `string` The value of the property to set. |

### SecureContext

**JSON representation**

```
{
  "secureParameterEntries": {
    object
  }
}
```

| Fields                   |                                                                                                                                                                                                                                                                                            |
|--------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `secureParameterEntries` | `object ( `[`Struct`](https://protobuf.dev/reference/protobuf/google.protobuf/#struct)` format)` Optional. A set of key-value pairs representing the secure parameter values. They can be retrieved via the SECURE_CONTEXT() function and used to modify the run-time behavior of a query. |

### JobConfigurationLoad

**JSON representation**

```
{
  "sourceUris": [
    string
  ],
  "fileSetSpecType": enum (FileSetSpecType),
  "schema": {
    object (TableSchema)
  },
  "destinationTable": {
    object (TableReference)
  },
  "destinationTableProperties": {
    object (DestinationTableProperties)
  },
  "createDisposition": string,
  "writeDisposition": string,
  "nullMarker": string,
  "fieldDelimiter": string,
  "skipLeadingRows": integer,
  "encoding": string,
  "quote": string,
  "maxBadRecords": integer,
  "schemaInlineFormat": string,
  "schemaInline": string,
  "allowQuotedNewlines": boolean,
  "sourceFormat": string,
  "allowJaggedRows": boolean,
  "ignoreUnknownValues": boolean,
  "projectionFields": [
    string
  ],
  "autodetect": boolean,
  "schemaUpdateOptions": [
    string
  ],
  "timePartitioning": {
    object (TimePartitioning)
  },
  "rangePartitioning": {
    object (RangePartitioning)
  },
  "clustering": {
    object (Clustering)
  },
  "destinationEncryptionConfiguration": {
    object (EncryptionConfiguration)
  },
  "useAvroLogicalTypes": boolean,
  "referenceFileSchemaUri": string,
  "hivePartitioningOptions": {
    object (HivePartitioningOptions)
  },
  "decimalTargetTypes": [
    enum (DecimalTargetType)
  ],
  "thriftOptions": {
    object (ThriftOptions)
  },
  "jsonExtension": enum (JsonExtension),
  "parquetOptions": {
    object (ParquetOptions)
  },
  "preserveAsciiControlCharacters": boolean,
  "connectionProperties": [
    {
      object (ConnectionProperty)
    }
  ],
  "createSession": boolean,
  "columnNameCharacterMap": enum (ColumnNameCharacterMap),
  "copyFilesOnly": boolean,
  "timeZone": string,
  "nullMarkers": [
    string
  ],
  "sourceColumnMatch": enum (SourceColumnMatch),
  "timestampTargetPrecision": [
    integer
  ],

  // Union field _date_format can be only one of the following:
  "dateFormat": string
  // End of list of possible types for union field _date_format.

  // Union field _datetime_format can be only one of the following:
  "datetimeFormat": string
  // End of list of possible types for union field _datetime_format.

  // Union field _time_format can be only one of the following:
  "timeFormat": string
  // End of list of possible types for union field _time_format.

  // Union field _timestamp_format can be only one of the following:
  "timestampFormat": string
  // End of list of possible types for union field _timestamp_format.
}
```

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
<td><code>sourceUris[]</code></td>
<td><p><code>string</code></p>
<p>[Required] The fully-qualified URIs that point to your data in Google Cloud. For Google Cloud Storage URIs: Each URI can contain one '*' wildcard character and it must come after the 'bucket' name. Size limits related to load jobs apply to external data sources. For Google Cloud Bigtable URIs: Exactly one URI can be specified and it has be a fully specified and valid HTTPS URL for a Google Cloud Bigtable table. For Google Cloud Datastore backups: Exactly one URI can be specified. Also, the '*' wildcard character is not allowed.</p></td>
</tr>
<tr class="even">
<td><code>fileSetSpecType</code></td>
<td><p><code>enum ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.FileSetSpecType"><code>FileSetSpecType</code></a><code> )</code></p>
<p>Optional. Specifies how source URIs are interpreted for constructing the file set to load. By default, source URIs are expanded against the underlying storage. You can also specify manifest files to control how the file set is constructed. This option is only applicable to object storage systems.</p></td>
</tr>
<tr class="odd">
<td><code>schema</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.TableSchema"><code>TableSchema</code></a><code> )</code></p>
<p>Optional. The schema for the destination table. The schema can be omitted if the destination table already exists, or if you're loading data from Google Cloud Datastore.</p></td>
</tr>
<tr class="even">
<td><code>destinationTable</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_dataset_info#Output.Schema.TableReference"><code>TableReference</code></a><code> )</code></p>
<p>[Required] The destination table to load the data into.</p></td>
</tr>
<tr class="odd">
<td><code>destinationTableProperties</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.DestinationTableProperties"><code>DestinationTableProperties</code></a><code> )</code></p>
<p>Optional. [Experimental] Properties with which to create the destination table if it is new.</p></td>
</tr>
<tr class="even">
<td><code>createDisposition</code></td>
<td><p><code>string</code></p>
<p>Optional. Specifies whether the job is allowed to create new tables. The following values are supported:</p>
<ul>
<li>CREATE_IF_NEEDED: If the table does not exist, BigQuery creates the table.</li>
<li>CREATE_NEVER: The table must already exist. If it does not, a 'notFound' error is returned in the job result. The default value is CREATE_IF_NEEDED. Creation, truncation and append actions occur as one atomic update upon job completion.</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>writeDisposition</code></td>
<td><p><code>string</code></p>
<p>Optional. Specifies the action that occurs if the destination table already exists. The following values are supported:</p>
<ul>
<li>WRITE_TRUNCATE: If the table already exists, BigQuery overwrites the data, removes the constraints and uses the schema from the load job.</li>
<li>WRITE_TRUNCATE_DATA: If the table already exists, BigQuery overwrites the data, but keeps the constraints and schema of the existing table.</li>
<li>WRITE_APPEND: If the table already exists, BigQuery appends the data to the table.</li>
<li>WRITE_EMPTY: If the table already exists and contains data, a 'duplicate' error is returned in the job result.</li>
</ul>
<p>The default value is WRITE_APPEND. Each action is atomic and only occurs if BigQuery is able to complete the job successfully. Creation, truncation and append actions occur as one atomic update upon job completion.</p></td>
</tr>
<tr class="even">
<td><code>nullMarker</code></td>
<td><p><code>string</code></p>
<p>Optional. Specifies a string that represents a null value in a CSV file. For example, if you specify "\N", BigQuery interprets "\N" as a null value when loading a CSV file. The default value is the empty string. If you set this property to a custom value, BigQuery throws an error if an empty string is present for all data types except for STRING and BYTE. For STRING and BYTE columns, BigQuery interprets the empty string as an empty value.</p></td>
</tr>
<tr class="odd">
<td><code>fieldDelimiter</code></td>
<td><p><code>string</code></p>
<p>Optional. The separator character for fields in a CSV file. The separator is interpreted as a single byte. For files encoded in ISO-8859-1, any single character can be used as a separator. For files encoded in UTF-8, characters represented in decimal range 1-127 (U+0001-U+007F) can be used without any modification. UTF-8 characters encoded with multiple bytes (i.e. U+0080 and above) will have only the first byte used for separating fields. The remaining bytes will be treated as a part of the field. BigQuery also supports the escape sequence "\t" (U+0009) to specify a tab separator. The default value is comma (",", U+002C).</p></td>
</tr>
<tr class="even">
<td><code>skipLeadingRows</code></td>
<td><p><code>integer</code></p>
<p>Optional. The number of rows at the top of a CSV file that BigQuery will skip when loading the data. The default value is 0. This property is useful if you have header rows in the file that should be skipped. When autodetect is on, the behavior is the following:</p>
<ul>
<li>skipLeadingRows unspecified - Autodetect tries to detect headers in the first row. If they are not detected, the row is read as data. Otherwise data is read starting from the second row.</li>
<li>skipLeadingRows is 0 - Instructs autodetect that there are no headers and data should be read starting from the first row.</li>
<li>skipLeadingRows = N &gt; 0 - Autodetect skips N-1 rows and tries to detect headers in row N. If headers are not detected, row N is just skipped. Otherwise row N is used to extract column names for the detected schema.</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>encoding</code></td>
<td><p><code>string</code></p>
<p>Optional. The character encoding of the data. The supported values are UTF-8, ISO-8859-1, UTF-16BE, UTF-16LE, UTF-32BE, and UTF-32LE. The default value is UTF-8. BigQuery decodes the data after the raw, binary data has been split using the values of the <code>quote</code> and <code>fieldDelimiter</code> properties.</p>
<p>If you don't specify an encoding, or if you specify a UTF-8 encoding when the CSV file is not UTF-8 encoded, BigQuery attempts to convert the data to UTF-8. Generally, your data loads successfully, but it may not match byte-for-byte what you expect. To avoid this, specify the correct encoding by using the <code>--encoding</code> flag.</p>
<p>If BigQuery can't convert a character other than the ASCII <code>0</code> character, BigQuery converts the character to the standard Unicode replacement character: �.</p></td>
</tr>
<tr class="even">
<td><code>quote</code></td>
<td><p><code>string</code></p>
<p>Optional. The value that is used to quote data sections in a CSV file. BigQuery converts the string to ISO-8859-1 encoding, and then uses the first byte of the encoded string to split the data in its raw, binary state. The default value is a double-quote ('"'). If your data does not contain quoted sections, set the property value to an empty string. If your data contains quoted newline characters, you must also set the allowQuotedNewlines property to true. To include the specific quote character within a quoted value, precede it with an additional matching quote character. For example, if you want to escape the default character ' " ', use ' "" '. @default "</p></td>
</tr>
<tr class="odd">
<td><code>maxBadRecords</code></td>
<td><p><code>integer</code></p>
<p>Optional. The maximum number of bad records that BigQuery can ignore when running the job. If the number of bad records exceeds this value, an invalid error is returned in the job result. The default value is 0, which requires that all records are valid. This is only supported for CSV and NEWLINE_DELIMITED_JSON file formats.</p></td>
</tr>
<tr class="even">
<td><code>schemaInlineFormat</code></td>
<td><p><code>string</code></p>
<p>[Deprecated] The format of the schemaInline property.</p></td>
</tr>
<tr class="odd">
<td><code>schemaInline</code></td>
<td><p><code>string</code></p>
<p>[Deprecated] The inline schema. For CSV schemas, specify as "Field1:Type1[,Field2:Type2]*". For example, "foo:STRING, bar:INTEGER, baz:FLOAT".</p></td>
</tr>
<tr class="even">
<td><code>allowQuotedNewlines</code></td>
<td><p><code>boolean</code></p>
<p>Indicates if BigQuery should allow quoted data sections that contain newline characters in a CSV file. The default value is false.</p></td>
</tr>
<tr class="odd">
<td><code>sourceFormat</code></td>
<td><p><code>string</code></p>
<p>Optional. The format of the data files. For CSV files, specify "CSV". For datastore backups, specify "DATASTORE_BACKUP". For newline-delimited JSON, specify "NEWLINE_DELIMITED_JSON". For Avro, specify "AVRO". For parquet, specify "PARQUET". For orc, specify "ORC". The default value is CSV.</p></td>
</tr>
<tr class="even">
<td><code>allowJaggedRows</code></td>
<td><p><code>boolean</code></p>
<p>Optional. Accept rows that are missing trailing optional columns. The missing values are treated as nulls. If false, records with missing trailing columns are treated as bad records, and if there are too many bad records, an invalid error is returned in the job result. The default value is false. Only applicable to CSV, ignored for other formats.</p></td>
</tr>
<tr class="odd">
<td><code>ignoreUnknownValues</code></td>
<td><p><code>boolean</code></p>
<p>Optional. Indicates if BigQuery should allow extra values that are not represented in the table schema. If true, the extra values are ignored. If false, records with extra columns are treated as bad records, and if there are too many bad records, an invalid error is returned in the job result. The default value is false. The sourceFormat property determines what BigQuery treats as an extra value: CSV: Trailing columns JSON: Named values that don't match any column names in the table schema Avro, Parquet, ORC: Fields in the file schema that don't exist in the table schema.</p></td>
</tr>
<tr class="even">
<td><code>projectionFields[]</code></td>
<td><p><code>string</code></p>
<p>If sourceFormat is set to "DATASTORE_BACKUP", indicates which entity properties to load into BigQuery from a Cloud Datastore backup. Property names are case sensitive and must be top-level properties. If no properties are specified, BigQuery loads all properties. If any named property isn't found in the Cloud Datastore backup, an invalid error is returned in the job result.</p></td>
</tr>
<tr class="odd">
<td><code>autodetect</code></td>
<td><p><code>boolean</code></p>
<p>Optional. Indicates if we should automatically infer the options and schema for CSV and JSON sources.</p></td>
</tr>
<tr class="even">
<td><code>schemaUpdateOptions[]</code></td>
<td><p><code>string</code></p>
<p>Allows the schema of the destination table to be updated as a side effect of the load job if a schema is autodetected or supplied in the job configuration. Schema update options are supported in three cases: when writeDisposition is WRITE_APPEND; when writeDisposition is WRITE_TRUNCATE_DATA; when writeDisposition is WRITE_TRUNCATE and the destination table is a partition of a table, specified by partition decorators. For normal tables, WRITE_TRUNCATE will always overwrite the schema. One or more of the following values are specified:</p>
<ul>
<li>ALLOW_FIELD_ADDITION: allow adding a nullable field to the schema.</li>
<li>ALLOW_FIELD_RELAXATION: allow relaxing a required field in the original schema to nullable.</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>timePartitioning</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.TimePartitioning"><code>TimePartitioning</code></a><code> )</code></p>
<p>Time-based partitioning specification for the destination table. Only one of timePartitioning and rangePartitioning should be specified.</p></td>
</tr>
<tr class="even">
<td><code>rangePartitioning</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.RangePartitioning"><code>RangePartitioning</code></a><code> )</code></p>
<p>Range partitioning specification for the destination table. Only one of timePartitioning and rangePartitioning should be specified.</p></td>
</tr>
<tr class="odd">
<td><code>clustering</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.Clustering"><code>Clustering</code></a><code> )</code></p>
<p>Clustering specification for the destination table.</p></td>
</tr>
<tr class="even">
<td><code>destinationEncryptionConfiguration</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_dataset_info#Output.Schema.EncryptionConfiguration"><code>EncryptionConfiguration</code></a><code> )</code></p>
<p>Custom encryption configuration (e.g., Cloud KMS keys)</p></td>
</tr>
<tr class="odd">
<td><code>useAvroLogicalTypes</code></td>
<td><p><code>boolean</code></p>
<p>Optional. If sourceFormat is set to "AVRO", indicates whether to interpret logical types as the corresponding BigQuery data type (for example, TIMESTAMP), instead of using the raw type (for example, INTEGER).</p></td>
</tr>
<tr class="even">
<td><code>referenceFileSchemaUri</code></td>
<td><p><code>string</code></p>
<p>Optional. The user can provide a reference file with the reader schema. This file is only loaded if it is part of source URIs, but is not loaded otherwise. It is enabled for the following formats: AVRO, PARQUET, ORC.</p></td>
</tr>
<tr class="odd">
<td><code>hivePartitioningOptions</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.HivePartitioningOptions"><code>HivePartitioningOptions</code></a><code> )</code></p>
<p>Optional. When set, configures hive partitioning support. Not all storage formats support hive partitioning -- requesting hive partitioning on an unsupported format will lead to an error, as will providing an invalid specification.</p></td>
</tr>
<tr class="even">
<td><code>decimalTargetTypes[]</code></td>
<td><p><code>enum ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.DecimalTargetType"><code>DecimalTargetType</code></a><code> )</code></p>
<p>Defines the list of possible SQL data types to which the source decimal values are converted. This list and the precision and the scale parameters of the decimal field determine the target type. In the order of NUMERIC, BIGNUMERIC, and STRING, a type is picked if it is in the specified list and if it supports the precision and the scale. STRING supports all precision and scale values. If none of the listed types supports the precision and the scale, the type supporting the widest range in the specified list is picked, and if a value exceeds the supported range when reading the data, an error will be thrown.</p>
<p>Example: Suppose the value of this field is ["NUMERIC", "BIGNUMERIC"]. If (precision,scale) is:</p>
<ul>
<li>(38,9) -&gt; NUMERIC;</li>
<li>(39,9) -&gt; BIGNUMERIC (NUMERIC cannot hold 30 integer digits);</li>
<li>(38,10) -&gt; BIGNUMERIC (NUMERIC cannot hold 10 fractional digits);</li>
<li>(76,38) -&gt; BIGNUMERIC;</li>
<li>(77,38) -&gt; BIGNUMERIC (error if value exceeds supported range).</li>
</ul>
<p>This field cannot contain duplicate types. The order of the types in this field is ignored. For example, ["BIGNUMERIC", "NUMERIC"] is the same as ["NUMERIC", "BIGNUMERIC"] and NUMERIC always takes precedence over BIGNUMERIC.</p>
<p>Defaults to ["NUMERIC", "STRING"] for ORC and ["NUMERIC"] for the other file formats.</p></td>
</tr>
<tr class="odd">
<td><code>thriftOptions</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.ThriftOptions"><code>ThriftOptions</code></a><code> )</code></p>
<p>Optional. [Experimental] The load options for Apache Thrift serialized data. It defines the source of IDL bundle that should be used to be parsed as the schema and deserialization options to parse Thrift data.</p></td>
</tr>
<tr class="even">
<td><code>jsonExtension</code></td>
<td><p><code>enum ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.JsonExtension"><code>JsonExtension</code></a><code> )</code></p>
<p>Optional. Load option to be used together with source_format newline-delimited JSON to indicate that a variant of JSON is being loaded. To load newline-delimited GeoJSON, specify GEOJSON (and source_format must be set to NEWLINE_DELIMITED_JSON).</p></td>
</tr>
<tr class="odd">
<td><code>parquetOptions</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.ParquetOptions"><code>ParquetOptions</code></a><code> )</code></p>
<p>Optional. Additional properties to set if sourceFormat is set to PARQUET.</p></td>
</tr>
<tr class="even">
<td><code>preserveAsciiControlCharacters</code></td>
<td><p><code>boolean</code></p>
<p>Optional. When sourceFormat is set to "CSV", this indicates whether the embedded ASCII control characters (the first 32 characters in the ASCII-table, from '\x00' to '\x1F') are preserved.</p></td>
</tr>
<tr class="odd">
<td><code>connectionProperties[]</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.ConnectionProperty"><code>ConnectionProperty</code></a><code> )</code></p>
<p>Optional. Connection properties which can modify the load job behavior. Currently, only the 'session_id' connection property is supported, and is used to resolve _SESSION appearing as the dataset id.</p></td>
</tr>
<tr class="even">
<td><code>createSession</code></td>
<td><p><code>boolean</code></p>
<p>Optional. If this property is true, the job creates a new session using a randomly generated session_id. To continue using a created session with subsequent queries, pass the existing session identifier as a <code>ConnectionProperty</code> value. The session identifier is returned as part of the <code>SessionInfo</code> message within the query statistics.</p>
<p>The new session's location will be set to <code>Job.JobReference.location</code> if it is present, otherwise it's set to the default location based on existing routing logic.</p></td>
</tr>
<tr class="odd">
<td><code>columnNameCharacterMap</code></td>
<td><p><code>enum ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.ColumnNameCharacterMap"><code>ColumnNameCharacterMap</code></a><code> )</code></p>
<p>Optional. Character map supported for column names in CSV/Parquet loads. Defaults to STRICT and can be overridden by Project Config Service. Using this option with unsupporting load formats will result in an error.</p></td>
</tr>
<tr class="even">
<td><code>copyFilesOnly</code></td>
<td><p><code>boolean</code></p>
<p>Optional. [Experimental] Configures the load job to copy files directly to the destination BigLake managed table, bypassing file content reading and rewriting.</p>
<p>Copying files only is supported when all the following are true:</p>
<ul>
<li><code>source_uris</code> are located in the same Cloud Storage location as the destination table's <code>storage_uri</code> location.</li>
<li><code>source_format</code> is <code>PARQUET</code> .</li>
<li><code>destination_table</code> is an existing BigLake managed table. The table's schema does not have flexible column names. The table's columns do not have type parameters other than precision and scale.</li>
<li>No options other than the above are specified.</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>timeZone</code></td>
<td><p><code>string</code></p>
<p>Optional. Default time zone that will apply when parsing timestamp values that have no specific time zone.</p></td>
</tr>
<tr class="even">
<td><code>nullMarkers[]</code></td>
<td><p><code>string</code></p>
<p>Optional. A list of strings represented as SQL NULL value in a CSV file.</p>
<p>null_marker and null_markers can't be set at the same time. If null_marker is set, null_markers has to be not set. If null_markers is set, null_marker has to be not set. If both null_marker and null_markers are set at the same time, a user error would be thrown. Any strings listed in null_markers, including empty string would be interpreted as SQL NULL. This applies to all column types.</p></td>
</tr>
<tr class="odd">
<td><code>sourceColumnMatch</code></td>
<td><p><code>enum ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.SourceColumnMatch"><code>SourceColumnMatch</code></a><code> )</code></p>
<p>Optional. Controls the strategy used to match loaded columns to the schema. If not set, a sensible default is chosen based on how the schema is provided. If autodetect is used, then columns are matched by name. Otherwise, columns are matched by position. This is done to keep the behavior backward-compatible.</p></td>
</tr>
<tr class="even">
<td><code>timestampTargetPrecision[]</code></td>
<td><p><code>integer</code></p>
<p>Precisions (maximum number of total digits in base 10) for seconds of TIMESTAMP types that are allowed to the destination table for autodetection mode.</p>
<p>Available for the formats: CSV, PARQUET, AVRO, and Iceberg External Table.</p>
<p>Possible values include: Not Specified, [], or [6]: timestamp(6) for all auto detected TIMESTAMP columns [6, 12]: timestamp(6) for all auto detected TIMESTAMP columns that have less than 6 digits of subseconds. timestamp(12) for all auto detected TIMESTAMP columns that have more than 6 digits of subseconds. [12]: timestamp(12) for all auto detected TIMESTAMP columns.</p>
<p>The order of the elements in this array is ignored. Inputs that have higher precision than the highest target precision in this array will be truncated.</p></td>
</tr>
<tr class="odd">
<td><p>Union field <code>_date_format</code> .</p>
<p><code>_date_format</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="even">
<td><code>dateFormat</code></td>
<td><p><code>string</code></p>
<p>Optional. Date format used for parsing DATE values.</p></td>
</tr>
<tr class="odd">
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p>Union field <code>_datetime_format</code> .</p>
<p><code>_datetime_format</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="odd">
<td><code>datetimeFormat</code></td>
<td><p><code>string</code></p>
<p>Optional. Date format used for parsing DATETIME values.</p></td>
</tr>
<tr class="even">
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p>Union field <code>_time_format</code> .</p>
<p><code>_time_format</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="even">
<td><code>timeFormat</code></td>
<td><p><code>string</code></p>
<p>Optional. Date format used for parsing TIME values.</p></td>
</tr>
<tr class="odd">
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p>Union field <code>_timestamp_format</code> .</p>
<p><code>_timestamp_format</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="odd">
<td><code>timestampFormat</code></td>
<td><p><code>string</code></p>
<p>Optional. Date format used for parsing TIMESTAMP values.</p></td>
</tr>
<tr class="even">
<td></td>
<td></td>
</tr>
</tbody>
</table>

### DestinationTableProperties

**JSON representation**

```
{
  "friendlyName": string,
  "description": string,
  "labels": {
    string: string,
    ...
  }
}
```

| Fields         |                                                                                                                                                                                                                                                                                                                                                                                                                                                |
|----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `friendlyName` | `string` Optional. Friendly name for the destination table. If the table already exists, it should be same as the existing friendly name.                                                                                                                                                                                                                                                                                                      |
| `description`  | `string` Optional. The description for the destination table. This will only be used if the destination table is newly created. If the table already exists and a value different than the current description is provided, the job will fail.                                                                                                                                                                                                 |
| `labels`       | `map (key: string, value: string)` Optional. The labels associated with this table. You can use these to organize and group your tables. This will only be used if the destination table is newly created. If the table already exists and labels are different than the current labels are provided, the job will fail. An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` . |

### LabelsEntry

**JSON representation**

```
{
  "key": string,
  "value": string
}
```

| Fields  |          |
|---------|----------|
| `key`   | `string` |
| `value` | `string` |

### ThriftOptions

**JSON representation**

```
{
  "schemaIdlRootDir": string,
  "schemaIdlUri": string,
  "schemaStruct": string,
  "deserializationOption": enum (DeserializationOption),
  "framingOption": enum (FramingOption),
  "boundaryBytes": string
}
```

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
<td><code>schemaIdlRootDir</code></td>
<td><p><code>string</code></p>
<p>Required. The root directory of the IDL file bundle defining the schema. All IDL files that are used to parse the schema should be in this directory. This directory should be different from the source_uris.</p></td>
</tr>
<tr class="even">
<td><code>schemaIdlUri</code></td>
<td><p><code>string</code></p>
<p>Required. The Thrift IDL file in the <code>schema_idl_root_dir</code> that should be used as the root file to parse the schema. All included idl files in the <code>schema_idl_uri</code> should also be in the <code>schema_idl_root_dir</code> or its sub-directory.</p></td>
</tr>
<tr class="odd">
<td><code>schemaStruct</code></td>
<td><p><code>string</code></p>
<p>Required. The root struct specified in <code>schema_idl_uri</code> that should be used to parse the schema.</p></td>
</tr>
<tr class="even">
<td><code>deserializationOption</code></td>
<td><p><code>enum ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.DeserializationOption"><code>DeserializationOption</code></a><code> )</code></p>
<p>Optional. <code>deserialization_option</code> sets how the serialized Thrift should be deserialized. The following options are supported:</p>
<ul>
<li>THRIFT_BINARY_PROTOCOL_OPTION: using TBinaryProtocol to deserialize the data.</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>framingOption</code></td>
<td><p><code>enum ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.FramingOption"><code>FramingOption</code></a><code> )</code></p>
<p>Optional. Framing in Thrift means 4 bytes slipped in front of the serialized record or data block to inidicate the size of the followed record or data block. The following options are support:</p>
<ul>
<li><p>NOT_FRAMED: Serialized Thrift records or data blocks are not framed, there are no 4-byte record size in front of the record.</p></li>
<li><p>FRAMED_WITH_BIG_ENDIAN: Serialized Thrift records or data blocks are framed with the 4-byte record size in big endian.</p></li>
<li><p>FRAMED_WITH_LITTLE_ENDIAN: Serialized Thrift records or data blocks are framed with the 4-byte record size in little endian.</p></li>
</ul>
<p>One option to frame Thrift record at serialization time is using <code>TFramedTransport</code> , which writes the 4-byte record or data block size in big endian. By default <code>framing_option</code> is set to "NOT_FRAMED".</p></td>
</tr>
<tr class="even">
<td><code>boundaryBytes</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>bytes</code></a><code> format)</code></p>
<p>Optional. Sequence of bytes used to separate two serialized Thrift data blocks. When it's used with <code>framing_option</code> , the <code>boundary_bytes</code> are expected to be in front of the framed block.</p>
<p>A base64-encoded string.</p></td>
</tr>
</tbody>
</table>

### JobConfigurationTableCopy

**JSON representation**

```
{
  "sourceTable": {
    object (TableReference)
  },
  "sourceTables": [
    {
      object (TableReference)
    }
  ],
  "destinationTable": {
    object (TableReference)
  },
  "createDisposition": string,
  "writeDisposition": string,
  "destinationEncryptionConfiguration": {
    object (EncryptionConfiguration)
  },
  "operationType": enum (OperationType),
  "destinationExpirationTime": string
}
```

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
<td><code>sourceTable</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_dataset_info#Output.Schema.TableReference"><code>TableReference</code></a><code> )</code></p>
<p>[Pick one] Source table to copy.</p></td>
</tr>
<tr class="even">
<td><code>sourceTables[]</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_dataset_info#Output.Schema.TableReference"><code>TableReference</code></a><code> )</code></p>
<p>[Pick one] Source tables to copy.</p></td>
</tr>
<tr class="odd">
<td><code>destinationTable</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_dataset_info#Output.Schema.TableReference"><code>TableReference</code></a><code> )</code></p>
<p>[Required] The destination table.</p></td>
</tr>
<tr class="even">
<td><code>createDisposition</code></td>
<td><p><code>string</code></p>
<p>Optional. Specifies whether the job is allowed to create new tables. The following values are supported:</p>
<ul>
<li>CREATE_IF_NEEDED: If the table does not exist, BigQuery creates the table.</li>
<li>CREATE_NEVER: The table must already exist. If it does not, a 'notFound' error is returned in the job result.</li>
</ul>
<p>The default value is CREATE_IF_NEEDED. Creation, truncation and append actions occur as one atomic update upon job completion.</p></td>
</tr>
<tr class="odd">
<td><code>writeDisposition</code></td>
<td><p><code>string</code></p>
<p>Optional. Specifies the action that occurs if the destination table already exists. The following values are supported:</p>
<ul>
<li>WRITE_TRUNCATE: If the table already exists, BigQuery overwrites the table data and uses the schema and table constraints from the source table.</li>
<li>WRITE_APPEND: If the table already exists, BigQuery appends the data to the table.</li>
<li>WRITE_EMPTY: If the table already exists and contains data, a 'duplicate' error is returned in the job result.</li>
</ul>
<p>The default value is WRITE_EMPTY. Each action is atomic and only occurs if BigQuery is able to complete the job successfully. Creation, truncation and append actions occur as one atomic update upon job completion.</p></td>
</tr>
<tr class="even">
<td><code>destinationEncryptionConfiguration</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_dataset_info#Output.Schema.EncryptionConfiguration"><code>EncryptionConfiguration</code></a><code> )</code></p>
<p>Custom encryption configuration (e.g., Cloud KMS keys).</p></td>
</tr>
<tr class="odd">
<td><code>operationType</code></td>
<td><p><code>enum ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.OperationType"><code>OperationType</code></a><code> )</code></p>
<p>Optional. Supported operation types in table copy job.</p></td>
</tr>
<tr class="even">
<td><code>destinationExpirationTime</code></td>
<td><p><code>string ( </code><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp"><code>Timestamp</code></a><code> format)</code></p>
<p>Optional. The time when the destination table expires. Expired tables will be deleted and their storage reclaimed.</p>
<p>Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: <code>"2014-10-02T15:01:23Z"</code> , <code>"2014-10-02T15:01:23.045123456Z"</code> or <code>"2014-10-02T15:01:23+05:30"</code> .</p></td>
</tr>
</tbody>
</table>

### Timestamp

**JSON representation**

```
{
  "seconds": string,
  "nanos": integer
}
```

| Fields    |                                                                                                                                                                                                                                                                                                                      |
|-----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `seconds` | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Represents seconds of UTC time since Unix epoch 1970-01-01T00:00:00Z. Must be between -62135596800 and 253402300799 inclusive (which corresponds to 0001-01-01T00:00:00Z to 9999-12-31T23:59:59Z).                            |
| `nanos`   | `integer` Non-negative fractions of a second at nanosecond resolution. This field is the nanosecond portion of the duration, not an alternative to seconds. Negative second values with fractions must still have non-negative nanos values that count forward in time. Must be between 0 and 999,999,999 inclusive. |

### JobConfigurationExtract

**JSON representation**

```
{
  "destinationUri": string,
  "destinationUris": [
    string
  ],
  "printHeader": boolean,
  "fieldDelimiter": string,
  "destinationFormat": string,
  "compression": string,
  "useAvroLogicalTypes": boolean,
  "modelExtractOptions": {
    object (ModelExtractOptions)
  },
  "nativeGeographyExportEnabled": boolean,
  "secureContext": {
    object (SecureContext)
  },

  // Union field source can be only one of the following:
  "sourceTable": {
    object (TableReference)
  },
  "sourceModel": {
    object (ModelReference)
  }
  // End of list of possible types for union field source.
}
```

| Fields                                                                                                       |                                                                                                                                                                                                                                                                                                                                                                                                                                              |
|--------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `destinationUri`                                                                                             | `string` \[Pick one\] DEPRECATED: Use destinationUris instead, passing only one URI as necessary. The fully-qualified Google Cloud Storage URI where the extracted table should be written.                                                                                                                                                                                                                                                  |
| `destinationUris[]`                                                                                          | `string` \[Pick one\] A list of fully-qualified Google Cloud Storage URIs where the extracted table should be written.                                                                                                                                                                                                                                                                                                                       |
| `printHeader`                                                                                                | `boolean` Optional. Whether to print out a header row in the results. Default is true. Not applicable when extracting models.                                                                                                                                                                                                                                                                                                                |
| `fieldDelimiter`                                                                                             | `string` Optional. When extracting data in CSV format, this defines the delimiter to use between fields in the exported data. Default is ','. Not applicable when extracting models.                                                                                                                                                                                                                                                         |
| `destinationFormat`                                                                                          | `string` Optional. The exported file format. Possible values include CSV, NEWLINE_DELIMITED_JSON, PARQUET, or AVRO for tables and ML_TF_SAVED_MODEL or ML_XGBOOST_BOOSTER for models. The default value for tables is CSV. Tables with nested or repeated fields cannot be exported as CSV. The default value for models is ML_TF_SAVED_MODEL.                                                                                               |
| `compression`                                                                                                | `string` Optional. The compression type to use for exported files. Possible values include DEFLATE, GZIP, NONE, SNAPPY, and ZSTD. The default value is NONE. Not all compression formats are support for all file formats. DEFLATE is only supported for Avro. ZSTD is only supported for Parquet. Not applicable when extracting models.                                                                                                    |
| `useAvroLogicalTypes`                                                                                        | `boolean` Whether to use logical types when extracting to AVRO format. Not applicable when extracting models.                                                                                                                                                                                                                                                                                                                                |
| `modelExtractOptions`                                                                                        | `object ( `[`ModelExtractOptions`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.ModelExtractOptions)` )` Optional. Model extract options only applicable when extracting models.                                                                                                                                                                                                            |
| `nativeGeographyExportEnabled`                                                                               | `boolean` Optional. Applicable to formats: PARQUET. If enabled, BigQuery to Parquet export will write the native Parquet Geography type instead of the default GeoParquet type.                                                                                                                                                                                                                                                              |
| `secureContext`                                                                                              | `object ( `[`SecureContext`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.SecureContext)` )` Optional. A set of key-value pairs representing the secure context. This can be used to pass sensitive or context-specific information. They can be retrieved via the SECURE_CONTEXT() function and used to modify the run-time behavior of an extract job on tables with row access policies. |
| Union field `source` . Required. Source reference for the export. `source` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| `sourceTable`                                                                                                | `object ( `[`TableReference`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_dataset_info#Output.Schema.TableReference)` )` A reference to the table being exported.                                                                                                                                                                                                                                               |
| `sourceModel`                                                                                                | `object ( `[`ModelReference`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.ModelReference)` )` A reference to the model being exported.                                                                                                                                                                                                                                                     |
|                                                                                                              |                                                                                                                                                                                                                                                                                                                                                                                                                                              |

### ModelReference

**JSON representation**

```
{
  "projectId": string,
  "datasetId": string,
  "modelId": string
}
```

| Fields      |                                                                                                                                                                  |
|-------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `projectId` | `string` Required. The ID of the project containing this model.                                                                                                  |
| `datasetId` | `string` Required. The ID of the dataset containing this model.                                                                                                  |
| `modelId`   | `string` Required. The ID of the model. The ID must contain only letters (a-z, A-Z), numbers (0-9), or underscores (\_). The maximum length is 1,024 characters. |

### ModelExtractOptions

**JSON representation**

```
{
  "trialId": string
}
```

| Fields    |                                                                                                                                                                                                                                                                                                                                                                                                                 |
|-----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `trialId` | `string ( `[`Int64Value`](https://developers.google.com/discovery/v1/type-format)` format)` The 1-based ID of the trial to be exported from a hyperparameter tuning model. If not specified, the trial with id = [Model](https://cloud.google.com/bigquery/docs/reference/rest/v2/models#resource:-model) .defaultTrialId is exported. This field is ignored for models not trained with hyperparameter tuning. |

### LabelsEntry

**JSON representation**

```
{
  "key": string,
  "value": string
}
```

| Fields  |          |
|---------|----------|
| `key`   | `string` |
| `value` | `string` |

### JobReference

**JSON representation**

```
{
  "projectId": string,
  "jobId": string,
  "location": string
}
```

| Fields      |                                                                                                                                                                                        |
|-------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `projectId` | `string` Required. The ID of the project containing this job.                                                                                                                          |
| `jobId`     | `string` Required. The ID of the job. The ID must contain only letters (a-z, A-Z), numbers (0-9), underscores (\_), or dashes (-). The maximum length is 1,024 characters.             |
| `location`  | `string` Optional. The geographic location of the job. The default value is US. For more information about BigQuery locations, see: <https://cloud.google.com/bigquery/docs/locations> |

### JobStatistics

**JSON representation**

```
{
  "creationTime": string,
  "startTime": string,
  "endTime": string,
  "totalBytesProcessed": string,
  "completionRatio": number,
  "quotaDeferments": [
    string
  ],
  "query": {
    object (JobStatistics2)
  },
  "load": {
    object (JobStatistics3)
  },
  "extract": {
    object (JobStatistics4)
  },
  "copy": {
    object (CopyJobStatistics)
  },
  "totalSlotMs": string,
  "reservationUsage": [
    {
      object (ReservationResourceUsage)
    }
  ],
  "reservation_id": string,
  "numChildJobs": string,
  "parentJobId": string,
  "scriptStatistics": {
    object (ScriptStatistics)
  },
  "rowLevelSecurityStatistics": {
    object (RowLevelSecurityStatistics)
  },
  "dataMaskingStatistics": {
    object (DataMaskingStatistics)
  },
  "transactionInfo": {
    object (TransactionInfo)
  },
  "sessionInfo": {
    object (SessionInfo)
  },
  "finalExecutionDurationMs": string,
  "edition": enum (ReservationEdition),
  "reservationGroupPath": [
    string
  ],
  "globalQueryRemoteRegions": [
    string
  ],
  "parentGlobalQueryJob": {
    object (JobReference)
  }
}
```

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
<td><code>creationTime</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>int64</code></a><code> format)</code></p>
<p>Output only. Creation time of this job, in milliseconds since the epoch. This field will be present on all jobs.</p></td>
</tr>
<tr class="even">
<td><code>startTime</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>int64</code></a><code> format)</code></p>
<p>Output only. Start time of this job, in milliseconds since the epoch. This field will be present when the job transitions from the PENDING state to either RUNNING or DONE.</p></td>
</tr>
<tr class="odd">
<td><code>endTime</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>int64</code></a><code> format)</code></p>
<p>Output only. End time of this job, in milliseconds since the epoch. This field will be present whenever a job is in the DONE state.</p></td>
</tr>
<tr class="even">
<td><code>totalBytesProcessed</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>Int64Value</code></a><code> format)</code></p>
<p>Output only. Total bytes processed for the job.</p></td>
</tr>
<tr class="odd">
<td><code>completionRatio</code></td>
<td><p><code>number</code></p>
<p>Output only. [TrustedTester] Job progress (0.0 -&gt; 1.0) for LOAD and EXTRACT jobs.</p></td>
</tr>
<tr class="even">
<td><code>quotaDeferments[]</code></td>
<td><p><code>string</code></p>
<p>Output only. Quotas which delayed this job's start time.</p></td>
</tr>
<tr class="odd">
<td><code>query</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.JobStatistics2"><code>JobStatistics2</code></a><code> )</code></p>
<p>Output only. Statistics for a query job.</p></td>
</tr>
<tr class="even">
<td><code>load</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.JobStatistics3"><code>JobStatistics3</code></a><code> )</code></p>
<p>Output only. Statistics for a load job.</p></td>
</tr>
<tr class="odd">
<td><code>extract</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.JobStatistics4"><code>JobStatistics4</code></a><code> )</code></p>
<p>Output only. Statistics for an extract job.</p></td>
</tr>
<tr class="even">
<td><code>copy</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.CopyJobStatistics"><code>CopyJobStatistics</code></a><code> )</code></p>
<p>Output only. Statistics for a copy job.</p></td>
</tr>
<tr class="odd">
<td><code>totalSlotMs</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>Int64Value</code></a><code> format)</code></p>
<p>Output only. Slot-milliseconds for the job.</p></td>
</tr>
<tr class="even">
<td><code>reservationUsage[] </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.ReservationResourceUsage"><code>ReservationResourceUsage</code></a><code> )</code></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>Output only. Job resource usage breakdown by reservation. This field reported misleading information and will no longer be populated.</p></td>
</tr>
<tr class="odd">
<td><code>reservation_id</code></td>
<td><p><code>string</code></p>
<p>Output only. Name of the primary reservation assigned to this job. Note that this could be different than reservations reported in the reservation usage field if parent reservations were used to execute this job.</p></td>
</tr>
<tr class="even">
<td><code>numChildJobs</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>int64</code></a><code> format)</code></p>
<p>Output only. Number of child jobs executed.</p></td>
</tr>
<tr class="odd">
<td><code>parentJobId</code></td>
<td><p><code>string</code></p>
<p>Output only. If this is a child job, specifies the job ID of the parent.</p></td>
</tr>
<tr class="even">
<td><code>scriptStatistics</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.ScriptStatistics"><code>ScriptStatistics</code></a><code> )</code></p>
<p>Output only. If this a child job of a script, specifies information about the context of this job within the script.</p></td>
</tr>
<tr class="odd">
<td><code>rowLevelSecurityStatistics</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.RowLevelSecurityStatistics"><code>RowLevelSecurityStatistics</code></a><code> )</code></p>
<p>Output only. Statistics for row-level security. Present only for query and extract jobs.</p></td>
</tr>
<tr class="even">
<td><code>dataMaskingStatistics</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.DataMaskingStatistics"><code>DataMaskingStatistics</code></a><code> )</code></p>
<p>Output only. Statistics for data-masking. Present only for query and extract jobs.</p></td>
</tr>
<tr class="odd">
<td><code>transactionInfo</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.TransactionInfo"><code>TransactionInfo</code></a><code> )</code></p>
<p>Output only. [Alpha] Information of the multi-statement transaction if this job is part of one.</p>
<p>This property is only expected on a child job or a job that is in a session. A script parent job is not part of the transaction started in the script.</p></td>
</tr>
<tr class="even">
<td><code>sessionInfo</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.SessionInfo"><code>SessionInfo</code></a><code> )</code></p>
<p>Output only. Information of the session if this job is part of one.</p></td>
</tr>
<tr class="odd">
<td><code>finalExecutionDurationMs</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>int64</code></a><code> format)</code></p>
<p>Output only. The duration in milliseconds of the execution of the final attempt of this job, as BigQuery may internally re-attempt to execute the job.</p></td>
</tr>
<tr class="even">
<td><code>edition</code></td>
<td><p><code>enum ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.ReservationEdition"><code>ReservationEdition</code></a><code> )</code></p>
<p>Output only. Name of edition corresponding to the reservation for this job at the time of this update.</p></td>
</tr>
<tr class="odd">
<td><code>reservationGroupPath[]</code></td>
<td><p><code>string</code></p>
<p>Output only. The reservation group path of the reservation assigned to this job. This field has a limit of 10 nested reservation groups. This is to maintain consistency between reservations info schema and jobs info schema. The first reservation group is the root reservation group and the last is the leaf or lowest level reservation group.</p></td>
</tr>
<tr class="even">
<td><code>globalQueryRemoteRegions[]</code></td>
<td><p><code>string</code></p>
<p>Output only. The list of remote regions from which a global query accesses data.</p>
<p>This field is populated only for parent global query jobs in the primary execution region. It is empty for child global query jobs and single-region queries. For more information, see <a href="https://cloud.google.com/bigquery/docs/global-queries">Global queries</a> .</p></td>
</tr>
<tr class="odd">
<td><code>parentGlobalQueryJob</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.JobReference"><code>JobReference</code></a><code> )</code></p>
<p>Output only. Reference to the parent global query job, if this is a child global query job.</p>
<p>This field is populated only for child global query jobs (remote subqueries or cross-region table copy jobs) executed in remote regions on behalf of a global query. It contains the project ID, job ID, and location of the parent global query job. It is unset for parent global query jobs and single-region queries. For more information, see <a href="https://cloud.google.com/bigquery/docs/global-queries">Global queries</a> .</p></td>
</tr>
</tbody>
</table>

### DoubleValue

**JSON representation**

```
{
  "value": number
}
```

| Fields  |                            |
|---------|----------------------------|
| `value` | `number` The double value. |

### JobStatistics2

**JSON representation**

```
{
  "queryPlan": [
    {
      object (ExplainQueryStage)
    }
  ],
  "estimatedBytesProcessed": string,
  "timeline": [
    {
      object (QueryTimelineSample)
    }
  ],
  "totalPartitionsProcessed": string,
  "totalBytesProcessed": string,
  "totalBytesProcessedAccuracy": string,
  "totalBytesBilled": string,
  "billingTier": integer,
  "totalSlotMs": string,
  "reservationUsage": [
    {
      object (ReservationResourceUsage)
    }
  ],
  "cacheHit": boolean,
  "referencedTables": [
    {
      object (TableReference)
    }
  ],
  "referencedRoutines": [
    {
      object (RoutineReference)
    }
  ],
  "referencedLogicalViews": [
    {
      object (TableReference)
    }
  ],
  "referencedPropertyGraphs": [
    {
      object (PropertyGraphReference)
    }
  ],
  "schema": {
    object (TableSchema)
  },
  "numDmlAffectedRows": string,
  "dmlStats": {
    object (DmlStats)
  },
  "undeclaredQueryParameters": [
    {
      object (QueryParameter)
    }
  ],
  "statementType": string,
  "ddlOperationPerformed": string,
  "ddlTargetTable": {
    object (TableReference)
  },
  "ddlDestinationTable": {
    object (TableReference)
  },
  "ddlTargetRowAccessPolicy": {
    object (RowAccessPolicyReference)
  },
  "ddlAffectedRowAccessPolicyCount": string,
  "ddlTargetRoutine": {
    object (RoutineReference)
  },
  "ddlTargetDataset": {
    object (DatasetReference)
  },
  "mlStatistics": {
    object (MlStatistics)
  },
  "exportDataStatistics": {
    object (ExportDataStatistics)
  },
  "externalServiceCosts": [
    {
      object (ExternalServiceCost)
    }
  ],
  "biEngineStatistics": {
    object (BiEngineStatistics)
  },
  "loadQueryStatistics": {
    object (LoadQueryStatistics)
  },
  "dclTargetTable": {
    object (TableReference)
  },
  "dclTargetView": {
    object (TableReference)
  },
  "dclTargetDataset": {
    object (DatasetReference)
  },
  "searchStatistics": {
    object (SearchStatistics)
  },
  "vectorSearchStatistics": {
    object (VectorSearchStatistics)
  },
  "performanceInsights": {
    object (PerformanceInsights)
  },
  "queryInfo": {
    object (QueryInfo)
  },
  "sparkStatistics": {
    object (SparkStatistics)
  },
  "transferredBytes": string,
  "materializedViewStatistics": {
    object (MaterializedViewStatistics)
  },
  "metadataCacheStatistics": {
    object (MetadataCacheStatistics)
  },
  "incrementalResultStats": {
    object (IncrementalResultStats)
  },
  "genAiStats": {
    object (GenAiStats)
  },
  "objectStorageStats": [
    {
      object (ObjectStorageStats)
    }
  ],

  // Union field _total_services_sku_slot_ms can be only one of the following:
  "totalServicesSkuSlotMs": string
  // End of list of possible types for union field _total_services_sku_slot_ms.
}
```

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
<td><code>queryPlan[]</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.ExplainQueryStage"><code>ExplainQueryStage</code></a><code> )</code></p>
<p>Output only. Describes execution plan for the query.</p></td>
</tr>
<tr class="even">
<td><code>estimatedBytesProcessed</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>Int64Value</code></a><code> format)</code></p>
<p>Output only. The original estimate of bytes processed for the job.</p></td>
</tr>
<tr class="odd">
<td><code>timeline[]</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.QueryTimelineSample"><code>QueryTimelineSample</code></a><code> )</code></p>
<p>Output only. Describes a timeline of job execution.</p></td>
</tr>
<tr class="even">
<td><code>totalPartitionsProcessed</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>Int64Value</code></a><code> format)</code></p>
<p>Output only. Total number of partitions processed from all partitioned tables referenced in the job.</p></td>
</tr>
<tr class="odd">
<td><code>totalBytesProcessed</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>Int64Value</code></a><code> format)</code></p>
<p>Output only. Total bytes processed for the job.</p></td>
</tr>
<tr class="even">
<td><code>totalBytesProcessedAccuracy</code></td>
<td><p><code>string</code></p>
<p>Output only. For dry-run jobs, totalBytesProcessed is an estimate and this field specifies the accuracy of the estimate. Possible values can be: UNKNOWN: accuracy of the estimate is unknown. PRECISE: estimate is precise. LOWER_BOUND: estimate is lower bound of what the query would cost. UPPER_BOUND: estimate is upper bound of what the query would cost.</p></td>
</tr>
<tr class="odd">
<td><code>totalBytesBilled</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>Int64Value</code></a><code> format)</code></p>
<p>Output only. If the project is configured to use on-demand pricing, then this field contains the total bytes billed for the job. If the project is configured to use flat-rate pricing, then you are not billed for bytes and this field is informational only.</p></td>
</tr>
<tr class="even">
<td><code>billingTier</code></td>
<td><p><code>integer</code></p>
<p>Output only. Billing tier for the job. This is a BigQuery-specific concept which is not related to the Google Cloud notion of "free tier". The value here is a measure of the query's resource consumption relative to the amount of data scanned. For on-demand queries, the limit is 100, and all queries within this limit are billed at the standard on-demand rates. On-demand queries that exceed this limit will fail with a billingTierLimitExceeded error.</p></td>
</tr>
<tr class="odd">
<td><code>totalSlotMs</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>Int64Value</code></a><code> format)</code></p>
<p>Output only. Slot-milliseconds for the job.</p></td>
</tr>
<tr class="even">
<td><code>reservationUsage[] </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.ReservationResourceUsage"><code>ReservationResourceUsage</code></a><code> )</code></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>Output only. Job resource usage breakdown by reservation. This field reported misleading information and will no longer be populated.</p></td>
</tr>
<tr class="odd">
<td><code>cacheHit</code></td>
<td><p><code>boolean</code></p>
<p>Output only. Whether the query result was fetched from the query cache.</p></td>
</tr>
<tr class="even">
<td><code>referencedTables[]</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_dataset_info#Output.Schema.TableReference"><code>TableReference</code></a><code> )</code></p>
<p>Output only. Referenced tables for the job.</p></td>
</tr>
<tr class="odd">
<td><code>referencedRoutines[]</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_dataset_info#Output.Schema.RoutineReference"><code>RoutineReference</code></a><code> )</code></p>
<p>Output only. Referenced routines for the job.</p></td>
</tr>
<tr class="even">
<td><code>referencedLogicalViews[]</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_dataset_info#Output.Schema.TableReference"><code>TableReference</code></a><code> )</code></p>
<p>Output only. Referenced logical views for the job.</p></td>
</tr>
<tr class="odd">
<td><code>referencedPropertyGraphs[]</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.PropertyGraphReference"><code>PropertyGraphReference</code></a><code> )</code></p>
<p>Output only. Referenced property graphs for the job. Queries that reference more than 50 property graphs will not have a complete list.</p></td>
</tr>
<tr class="even">
<td><code>schema</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.TableSchema"><code>TableSchema</code></a><code> )</code></p>
<p>Output only. The schema of the results. Present only for successful dry run of non-legacy SQL queries.</p></td>
</tr>
<tr class="odd">
<td><code>numDmlAffectedRows</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>Int64Value</code></a><code> format)</code></p>
<p>Output only. The number of rows affected by a DML statement. Present only for DML statements INSERT, UPDATE or DELETE.</p></td>
</tr>
<tr class="even">
<td><code>dmlStats</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.DmlStats"><code>DmlStats</code></a><code> )</code></p>
<p>Output only. Detailed statistics for DML statements INSERT, UPDATE, DELETE, MERGE or TRUNCATE.</p></td>
</tr>
<tr class="odd">
<td><code>undeclaredQueryParameters[]</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.QueryParameter"><code>QueryParameter</code></a><code> )</code></p>
<p>Output only. GoogleSQL only: list of undeclared query parameters detected during a dry run validation.</p></td>
</tr>
<tr class="even">
<td><code>statementType</code></td>
<td><p><code>string</code></p>
<p>Output only. The type of query statement, if valid. Possible values:</p>
<ul>
<li><code>SELECT</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/query-syntax#select_list"><code>SELECT</code></a> statement.</li>
<li><code>ASSERT</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/debugging-statements#assert"><code>ASSERT</code></a> statement.</li>
<li><code>INSERT</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/dml-syntax#insert_statement"><code>INSERT</code></a> statement.</li>
<li><code>UPDATE</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/dml-syntax#update_statement"><code>UPDATE</code></a> statement.</li>
<li><code>DELETE</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-manipulation-language"><code>DELETE</code></a> statement.</li>
<li><code>MERGE</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-manipulation-language"><code>MERGE</code></a> statement.</li>
<li><code>TRUNCATE_TABLE</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/dml-syntax#truncate_table_statement"><code>TRUNCATE TABLE</code></a> statement.</li>
<li><code>CREATE_TABLE</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_table_statement"><code>CREATE TABLE</code></a> statement, without <code>AS SELECT</code> .</li>
<li><code>CREATE_TABLE_AS_SELECT</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_table_statement"><code>CREATE TABLE AS SELECT</code></a> statement.</li>
<li><code>CREATE_VIEW</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_view_statement"><code>CREATE VIEW</code></a> statement.</li>
<li><code>CREATE_MODEL</code> : <a href="https://cloud.google.com/bigquery-ml/docs/reference/standard-sql/bigqueryml-syntax-create#create_model_statement"><code>CREATE MODEL</code></a> statement.</li>
<li><code>CREATE_MATERIALIZED_VIEW</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_materialized_view_statement"><code>CREATE MATERIALIZED VIEW</code></a> statement.</li>
<li><code>CREATE_FUNCTION</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_function_statement"><code>CREATE FUNCTION</code></a> statement.</li>
<li><code>CREATE_TABLE_FUNCTION</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_table_function_statement"><code>CREATE TABLE FUNCTION</code></a> statement.</li>
<li><code>CREATE_PROCEDURE</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_procedure"><code>CREATE PROCEDURE</code></a> statement.</li>
<li><code>CREATE_ROW_ACCESS_POLICY</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_row_access_policy_statement"><code>CREATE ROW ACCESS POLICY</code></a> statement.</li>
<li><code>CREATE_SCHEMA</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_schema_statement"><code>CREATE SCHEMA</code></a> statement.</li>
<li><code>CREATE_EXTERNAL_SCHEMA</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_external_schema_statement"><code>CREATE EXTERNAL SCHEMA</code></a> statement.</li>
<li><code>CREATE_EXTERNAL_TABLE</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_external_table_statement"><code>CREATE EXTERNAL TABLE</code></a> statement.</li>
<li><code>CREATE_SNAPSHOT_TABLE</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_snapshot_table_statement"><code>CREATE SNAPSHOT TABLE</code></a> statement.</li>
<li><code>CREATE_SEARCH_INDEX</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_search_index_statement"><code>CREATE SEARCH INDEX</code></a> statement.</li>
<li><code>CREATE_VECTOR_INDEX</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_vector_index_statement"><code>CREATE VECTOR INDEX</code></a> statement.</li>
<li><code>CREATE_CONNECTION</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_connection_statement"><code>CREATE CONNECTION</code></a> statement.</li>
<li><code>CREATE_DATA_POLICY</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_data_policy_statement"><code>CREATE DATA_POLICY</code></a> statement.</li>
<li><code>CREATE_PROPERTY_GRAPH</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/graph-schema-statements#gql_create_graph"><code>CREATE PROPERTY GRAPH</code></a> statement.</li>
<li><code>CREATE_CAPACITY</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_capacity_statement"><code>CREATE CAPACITY</code></a> statement.</li>
<li><code>CREATE_RESERVATION</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_reservation_statement"><code>CREATE RESERVATION</code></a> statement.</li>
<li><code>CREATE_ASSIGNMENT</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_assignment_statement"><code>CREATE ASSIGNMENT</code></a> statement.</li>
<li><code>DROP_TABLE</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#drop_table_statement"><code>DROP TABLE</code></a> statement.</li>
<li><code>DROP_EXTERNAL_TABLE</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#drop_external_table_statement"><code>DROP EXTERNAL TABLE</code></a> statement.</li>
<li><code>DROP_VIEW</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#drop_view_statement"><code>DROP VIEW</code></a> statement.</li>
<li><code>DROP_MODEL</code> : <a href="https://cloud.google.com/bigquery-ml/docs/reference/standard-sql/bigqueryml-syntax-drop-model"><code>DROP MODEL</code></a> statement.</li>
<li><code>DROP_MATERIALIZED_VIEW</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#drop_materialized_view_statement"><code>DROP MATERIALIZED VIEW</code></a> statement.</li>
<li><code>DROP_FUNCTION</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#drop_function_statement"><code>DROP FUNCTION</code></a> statement.</li>
<li><code>DROP_TABLE_FUNCTION</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#drop_table_function"><code>DROP TABLE FUNCTION</code></a> statement.</li>
<li><code>DROP_PROCEDURE</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#drop_procedure_statement"><code>DROP PROCEDURE</code></a> statement.</li>
<li><code>DROP_SEARCH_INDEX</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#drop_search_index"><code>DROP SEARCH INDEX</code></a> statement.</li>
<li><code>DROP_VECTOR_INDEX</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#drop_vector_index"><code>DROP VECTOR INDEX</code></a> statement.</li>
<li><code>DROP_SCHEMA</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#drop_schema_statement"><code>DROP SCHEMA</code></a> statement.</li>
<li><code>UNDROP_SCHEMA</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#undrop_schema_statement"><code>UNDROP SCHEMA</code></a> statement.</li>
<li><code>DROP_SNAPSHOT_TABLE</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#drop_snapshot_table_statement"><code>DROP SNAPSHOT TABLE</code></a> statement.</li>
<li><code>DROP_ROW_ACCESS_POLICY</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#drop_row_access_policy_statement"><code>DROP [ALL] ROW ACCESS POLICY|POLICIES</code></a> statement.</li>
<li><code>DROP_CONNECTION</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#drop_connection_statement"><code>DROP CONNECTION</code></a> statement.</li>
<li><code>DROP_DATA_POLICY</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#drop_data_policy"><code>DROP DATA_POLICY</code></a> statement.</li>
<li><code>DROP_PROPERTY_GRAPH</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/graph-schema-statements#gql_drop_graph"><code>DROP PROPERTY GRAPH</code></a> statement.</li>
<li><code>DROP_CAPACITY</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#drop_capacity_statement"><code>DROP CAPACITY</code></a> statement.</li>
<li><code>DROP_RESERVATION</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#drop_reservation_statement"><code>DROP RESERVATION</code></a> statement.</li>
<li><code>DROP_ASSIGNMENT</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#drop_assignment_statement"><code>DROP ASSIGNMENT</code></a> statement.</li>
<li><code>ALTER_TABLE</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#alter_table_set_options_statement"><code>ALTER TABLE</code></a> statement.</li>
<li><code>ALTER_VIEW</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#alter_view_set_options_statement"><code>ALTER VIEW</code></a> statement.</li>
<li><code>ALTER_MATERIALIZED_VIEW</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#alter_materialized_view_set_options_statement"><code>ALTER MATERIALIZED VIEW</code></a> statement.</li>
<li><code>ALTER_SCHEMA</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#alter_schema_set_options_statement"><code>ALTER SCHEMA</code></a> statement.</li>
<li><code>ALTER_MODEL</code> : <a href="https://cloud.google.com/bigquery-ml/docs/reference/standard-sql/bigqueryml-syntax-alter-model"><code>ALTER MODEL</code></a> statement.</li>
<li><code>ALTER_SEARCH_INDEX</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#alter_search_index_statement"><code>ALTER SEARCH INDEX</code></a> statement.</li>
<li><code>ALTER_VECTOR_INDEX</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#alter_vector_index_rebuild_statement"><code>ALTER VECTOR INDEX</code></a> statement.</li>
<li><code>ALTER_CONNECTION</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#alter_connection_set_options_statement"><code>ALTER CONNECTION</code></a> statement.</li>
<li><code>ALTER_DATA_POLICY</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#alter_data_policy_statement"><code>ALTER DATA_POLICY</code></a> statement.</li>
<li><code>ALTER_PROJECT</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#alter_project_set_options_statement"><code>ALTER PROJECT</code></a> statement.</li>
<li><code>ALTER_ORGANIZATION</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#alter_organization_set_options_statement"><code>ALTER ORGANIZATION</code></a> statement.</li>
<li><code>ALTER_BI_CAPACITY</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#alter_bi_capacity_set_options_statement"><code>ALTER BI_CAPACITY</code></a> statement.</li>
<li><code>ALTER_CAPACITY</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#alter_capacity_set_options_statement"><code>ALTER CAPACITY</code></a> statement.</li>
<li><code>ALTER_RESERVATION</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#alter_reservation_set_options_statement"><code>ALTER RESERVATION</code></a> statement.</li>
<li><code>SCRIPT</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/procedural-language"><code>SCRIPT</code></a> statement.</li>
<li><code>CALL</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/procedural-language#call"><code>CALL</code></a> statement.</li>
<li><code>BEGIN_TRANSACTION</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/procedural-language#begin_transaction"><code>BEGIN TRANSACTION</code></a> statement.</li>
<li><code>COMMIT_TRANSACTION</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/procedural-language#commit_transaction"><code>COMMIT TRANSACTION</code></a> statement.</li>
<li><code>ROLLBACK_TRANSACTION</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/procedural-language#rollback_transaction"><code>ROLLBACK TRANSACTION</code></a> statement.</li>
<li><code>EXPORT_DATA</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/export-statements#export_data_statement"><code>EXPORT DATA</code></a> statement.</li>
<li><code>EXPORT_MODEL</code> : <a href="https://cloud.google.com/bigquery-ml/docs/reference/standard-sql/bigqueryml-syntax-export-model"><code>EXPORT MODEL</code></a> statement.</li>
<li><code>EXPORT_METADATA</code> : <a href="https://cloud.google.com/bigquery/docs/biglake-iceberg-tables-in-bigquery"><code>EXPORT TABLE METADATA</code></a> statement, for BigLake Iceberg tables.</li>
<li><code>LOAD_DATA</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/load-statements#load_data_statement"><code>LOAD DATA</code></a> statement.</li>
<li><code>GRANT_ON_SCHEMA</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-control-language#grant_statement"><code>GRANT ... ON SCHEMA</code></a> statement.</li>
<li><code>GRANT_ON_TABLE</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-control-language#grant_statement"><code>GRANT ... ON TABLE</code></a> statement. Also used for <code>GRANT ... ON EXTERNAL TABLE</code> .</li>
<li><code>GRANT_ON_VIEW</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-control-language#grant_statement"><code>GRANT ... ON VIEW</code></a> statement.</li>
<li><code>GRANT_ON_PROJECT</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-control-language#grant_statement"><code>GRANT ... ON PROJECT</code></a> statement.</li>
<li><code>REVOKE_ON_SCHEMA</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-control-language#revoke_statement"><code>REVOKE ... ON SCHEMA</code></a> statement.</li>
<li><code>REVOKE_ON_TABLE</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-control-language#revoke_statement"><code>REVOKE ... ON TABLE</code></a> statement. Also used for <code>REVOKE ... ON EXTERNAL TABLE</code> .</li>
<li><code>REVOKE_ON_VIEW</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-control-language#revoke_statement"><code>REVOKE ... ON VIEW</code></a> statement.</li>
<li><code>REVOKE_ON_PROJECT</code> : <a href="https://cloud.google.com/bigquery/docs/reference/standard-sql/data-control-language#revoke_statement"><code>REVOKE ... ON PROJECT</code></a> statement.</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>ddlOperationPerformed</code></td>
<td><p><code>string</code></p>
<p>Output only. The DDL operation performed, possibly dependent on the pre-existence of the DDL target.</p></td>
</tr>
<tr class="even">
<td><code>ddlTargetTable</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_dataset_info#Output.Schema.TableReference"><code>TableReference</code></a><code> )</code></p>
<p>Output only. The DDL target table. Present only for CREATE/DROP TABLE/VIEW and DROP ALL ROW ACCESS POLICIES queries.</p></td>
</tr>
<tr class="odd">
<td><code>ddlDestinationTable</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_dataset_info#Output.Schema.TableReference"><code>TableReference</code></a><code> )</code></p>
<p>Output only. The table after rename. Present only for ALTER TABLE RENAME TO query.</p></td>
</tr>
<tr class="even">
<td><code>ddlTargetRowAccessPolicy</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.RowAccessPolicyReference"><code>RowAccessPolicyReference</code></a><code> )</code></p>
<p>Output only. The DDL target row access policy. Present only for CREATE/DROP ROW ACCESS POLICY queries.</p></td>
</tr>
<tr class="odd">
<td><code>ddlAffectedRowAccessPolicyCount</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>Int64Value</code></a><code> format)</code></p>
<p>Output only. The number of row access policies affected by a DDL statement. Present only for DROP ALL ROW ACCESS POLICIES queries.</p></td>
</tr>
<tr class="even">
<td><code>ddlTargetRoutine</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_dataset_info#Output.Schema.RoutineReference"><code>RoutineReference</code></a><code> )</code></p>
<p>Output only. [Beta] The DDL target routine. Present only for CREATE/DROP FUNCTION/PROCEDURE queries.</p></td>
</tr>
<tr class="odd">
<td><code>ddlTargetDataset</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_dataset_info#Output.Schema.DatasetReference"><code>DatasetReference</code></a><code> )</code></p>
<p>Output only. The DDL target dataset. Present only for CREATE/ALTER/DROP SCHEMA(dataset) queries.</p></td>
</tr>
<tr class="even">
<td><code>mlStatistics</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.MlStatistics"><code>MlStatistics</code></a><code> )</code></p>
<p>Output only. Statistics of a BigQuery ML training job.</p></td>
</tr>
<tr class="odd">
<td><code>exportDataStatistics</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.ExportDataStatistics"><code>ExportDataStatistics</code></a><code> )</code></p>
<p>Output only. Stats for EXPORT DATA statement.</p></td>
</tr>
<tr class="even">
<td><code>externalServiceCosts[]</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.ExternalServiceCost"><code>ExternalServiceCost</code></a><code> )</code></p>
<p>Output only. Job cost breakdown as bigquery internal cost and external service costs.</p></td>
</tr>
<tr class="odd">
<td><code>biEngineStatistics</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.BiEngineStatistics"><code>BiEngineStatistics</code></a><code> )</code></p>
<p>Output only. BI Engine specific Statistics.</p></td>
</tr>
<tr class="even">
<td><code>loadQueryStatistics</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.LoadQueryStatistics"><code>LoadQueryStatistics</code></a><code> )</code></p>
<p>Output only. Statistics for a LOAD query.</p></td>
</tr>
<tr class="odd">
<td><code>dclTargetTable</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_dataset_info#Output.Schema.TableReference"><code>TableReference</code></a><code> )</code></p>
<p>Output only. Referenced table for DCL statement.</p></td>
</tr>
<tr class="even">
<td><code>dclTargetView</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_dataset_info#Output.Schema.TableReference"><code>TableReference</code></a><code> )</code></p>
<p>Output only. Referenced view for DCL statement.</p></td>
</tr>
<tr class="odd">
<td><code>dclTargetDataset</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_dataset_info#Output.Schema.DatasetReference"><code>DatasetReference</code></a><code> )</code></p>
<p>Output only. Referenced dataset for DCL statement.</p></td>
</tr>
<tr class="even">
<td><code>searchStatistics</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.SearchStatistics"><code>SearchStatistics</code></a><code> )</code></p>
<p>Output only. Search query specific statistics.</p></td>
</tr>
<tr class="odd">
<td><code>vectorSearchStatistics</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.VectorSearchStatistics"><code>VectorSearchStatistics</code></a><code> )</code></p>
<p>Output only. Vector Search query specific statistics.</p></td>
</tr>
<tr class="even">
<td><code>performanceInsights</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.PerformanceInsights"><code>PerformanceInsights</code></a><code> )</code></p>
<p>Output only. Performance insights.</p></td>
</tr>
<tr class="odd">
<td><code>queryInfo</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.QueryInfo"><code>QueryInfo</code></a><code> )</code></p>
<p>Output only. Query optimization information for a QUERY job.</p></td>
</tr>
<tr class="even">
<td><code>sparkStatistics</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.SparkStatistics"><code>SparkStatistics</code></a><code> )</code></p>
<p>Output only. Statistics of a Spark procedure job.</p></td>
</tr>
<tr class="odd">
<td><code>transferredBytes</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>Int64Value</code></a><code> format)</code></p>
<p>Output only. Total bytes transferred for BigQuery Omni queries from the remote cloud back to Google Cloud. This tracks data movement over Google-managed connections (like query results). It doesn't include input data read from the external data lake (for example, S3) because that data stays within the remote cloud.</p></td>
</tr>
<tr class="even">
<td><code>materializedViewStatistics</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.MaterializedViewStatistics"><code>MaterializedViewStatistics</code></a><code> )</code></p>
<p>Output only. Statistics of materialized views of a query job.</p></td>
</tr>
<tr class="odd">
<td><code>metadataCacheStatistics</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.MetadataCacheStatistics"><code>MetadataCacheStatistics</code></a><code> )</code></p>
<p>Output only. Statistics of metadata cache usage in a query for BigLake tables.</p></td>
</tr>
<tr class="even">
<td><code>incrementalResultStats</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.IncrementalResultStats"><code>IncrementalResultStats</code></a><code> )</code></p>
<p>Output only. Statistics related to incremental query results, if enabled for the query. This feature is not yet available.</p></td>
</tr>
<tr class="odd">
<td><code>genAiStats</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.GenAiStats"><code>GenAiStats</code></a><code> )</code></p>
<p>Output only. Statistics related to GenAI usage in the query.</p></td>
</tr>
<tr class="even">
<td><code>objectStorageStats[]</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.ObjectStorageStats"><code>ObjectStorageStats</code></a><code> )</code></p>
<p>Output only. Storage and caching statistics per cloud provider for queries over object storage.</p></td>
</tr>
<tr class="odd">
<td><p>Union field <code>_total_services_sku_slot_ms</code> .</p>
<p><code>_total_services_sku_slot_ms</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="even">
<td><code>totalServicesSkuSlotMs</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>int64</code></a><code> format)</code></p>
<p>Output only. Total slot milliseconds for the job that ran on external services and billed on the services SKU. This field is only populated for jobs that have external service costs, and is the total of the usage for costs whose billing method is <code>"SERVICES_SKU"</code> .</p></td>
</tr>
<tr class="odd">
<td></td>
<td></td>
</tr>
</tbody>
</table>

### ExplainQueryStage

**JSON representation**

```
{
  "name": string,
  "id": string,
  "startMs": string,
  "endMs": string,
  "inputStages": [
    string
  ],
  "waitRatioAvg": number,
  "waitMsAvg": string,
  "waitRatioMax": number,
  "waitMsMax": string,
  "readRatioAvg": number,
  "readMsAvg": string,
  "readRatioMax": number,
  "readMsMax": string,
  "computeRatioAvg": number,
  "computeMsAvg": string,
  "computeRatioMax": number,
  "computeMsMax": string,
  "writeRatioAvg": number,
  "writeMsAvg": string,
  "writeRatioMax": number,
  "writeMsMax": string,
  "shuffleOutputBytes": string,
  "shuffleOutputBytesSpilled": string,
  "recordsRead": string,
  "recordsWritten": string,
  "parallelInputs": string,
  "completedParallelInputs": string,
  "status": string,
  "steps": [
    {
      object (ExplainQueryStep)
    }
  ],
  "slotMs": string,
  "computeMode": enum (ComputeMode)
}
```

| Fields                      |                                                                                                                                                                                                                                            |
|-----------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`                      | `string` Human-readable name for the stage.                                                                                                                                                                                                |
| `id`                        | `string ( `[`Int64Value`](https://developers.google.com/discovery/v1/type-format)` format)` Unique ID for the stage within the plan.                                                                                                       |
| `startMs`                   | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Stage start time represented as milliseconds since the epoch.                                                                                       |
| `endMs`                     | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Stage end time represented as milliseconds since the epoch.                                                                                         |
| `inputStages[]`             | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` IDs for stages that are inputs to this stage.                                                                                                       |
| `waitRatioAvg`              | `number` Relative amount of time the average shard spent waiting to be scheduled.                                                                                                                                                          |
| `waitMsAvg`                 | `string ( `[`Int64Value`](https://developers.google.com/discovery/v1/type-format)` format)` Milliseconds the average shard spent waiting to be scheduled.                                                                                  |
| `waitRatioMax`              | `number` Relative amount of time the slowest shard spent waiting to be scheduled.                                                                                                                                                          |
| `waitMsMax`                 | `string ( `[`Int64Value`](https://developers.google.com/discovery/v1/type-format)` format)` Milliseconds the slowest shard spent waiting to be scheduled.                                                                                  |
| `readRatioAvg`              | `number` Relative amount of time the average shard spent reading input.                                                                                                                                                                    |
| `readMsAvg`                 | `string ( `[`Int64Value`](https://developers.google.com/discovery/v1/type-format)` format)` Milliseconds the average shard spent reading input.                                                                                            |
| `readRatioMax`              | `number` Relative amount of time the slowest shard spent reading input.                                                                                                                                                                    |
| `readMsMax`                 | `string ( `[`Int64Value`](https://developers.google.com/discovery/v1/type-format)` format)` Milliseconds the slowest shard spent reading input.                                                                                            |
| `computeRatioAvg`           | `number` Relative amount of time the average shard spent on CPU-bound tasks.                                                                                                                                                               |
| `computeMsAvg`              | `string ( `[`Int64Value`](https://developers.google.com/discovery/v1/type-format)` format)` Milliseconds the average shard spent on CPU-bound tasks.                                                                                       |
| `computeRatioMax`           | `number` Relative amount of time the slowest shard spent on CPU-bound tasks.                                                                                                                                                               |
| `computeMsMax`              | `string ( `[`Int64Value`](https://developers.google.com/discovery/v1/type-format)` format)` Milliseconds the slowest shard spent on CPU-bound tasks.                                                                                       |
| `writeRatioAvg`             | `number` Relative amount of time the average shard spent on writing output.                                                                                                                                                                |
| `writeMsAvg`                | `string ( `[`Int64Value`](https://developers.google.com/discovery/v1/type-format)` format)` Milliseconds the average shard spent on writing output.                                                                                        |
| `writeRatioMax`             | `number` Relative amount of time the slowest shard spent on writing output.                                                                                                                                                                |
| `writeMsMax`                | `string ( `[`Int64Value`](https://developers.google.com/discovery/v1/type-format)` format)` Milliseconds the slowest shard spent on writing output.                                                                                        |
| `shuffleOutputBytes`        | `string ( `[`Int64Value`](https://developers.google.com/discovery/v1/type-format)` format)` Total number of bytes written to shuffle.                                                                                                      |
| `shuffleOutputBytesSpilled` | `string ( `[`Int64Value`](https://developers.google.com/discovery/v1/type-format)` format)` Total number of bytes written to shuffle and spilled to disk.                                                                                  |
| `recordsRead`               | `string ( `[`Int64Value`](https://developers.google.com/discovery/v1/type-format)` format)` Number of records read into the stage.                                                                                                         |
| `recordsWritten`            | `string ( `[`Int64Value`](https://developers.google.com/discovery/v1/type-format)` format)` Number of records written by the stage.                                                                                                        |
| `parallelInputs`            | `string ( `[`Int64Value`](https://developers.google.com/discovery/v1/type-format)` format)` Number of parallel input segments to be processed                                                                                              |
| `completedParallelInputs`   | `string ( `[`Int64Value`](https://developers.google.com/discovery/v1/type-format)` format)` Number of parallel input segments completed.                                                                                                   |
| `status`                    | `string` Current status for this stage.                                                                                                                                                                                                    |
| `steps[]`                   | `object ( `[`ExplainQueryStep`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.ExplainQueryStep)` )` List of operations within the stage in dependency order (approximately chronological). |
| `slotMs`                    | `string ( `[`Int64Value`](https://developers.google.com/discovery/v1/type-format)` format)` Slot-milliseconds used by the stage.                                                                                                           |
| `computeMode`               | `enum ( `[`ComputeMode`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.ComputeMode)` )` Output only. Compute mode for this stage.                                                          |

### ExplainQueryStep

**JSON representation**

```
{
  "kind": string,
  "substeps": [
    string
  ]
}
```

| Fields       |                                                     |
|--------------|-----------------------------------------------------|
| `kind`       | `string` Machine-readable operation type.           |
| `substeps[]` | `string` Human-readable description of the step(s). |

### QueryTimelineSample

**JSON representation**

```
{
  "elapsedMs": string,
  "totalSlotMs": string,
  "pendingUnits": string,
  "completedUnits": string,
  "activeUnits": string,
  "shuffleRamUsageRatio": number,
  "estimatedRunnableUnits": string
}
```

| Fields                   |                                                                                                                                                                                                                                                                                         |
|--------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `elapsedMs`              | `string ( `[`Int64Value`](https://developers.google.com/discovery/v1/type-format)` format)` Milliseconds elapsed since the start of query execution.                                                                                                                                    |
| `totalSlotMs`            | `string ( `[`Int64Value`](https://developers.google.com/discovery/v1/type-format)` format)` Cumulative slot-ms consumed by the query.                                                                                                                                                   |
| `pendingUnits`           | `string ( `[`Int64Value`](https://developers.google.com/discovery/v1/type-format)` format)` Total units of work remaining for the query. This number can be revised (increased or decreased) while the query is running.                                                                |
| `completedUnits`         | `string ( `[`Int64Value`](https://developers.google.com/discovery/v1/type-format)` format)` Total parallel units of work completed by this query.                                                                                                                                       |
| `activeUnits`            | `string ( `[`Int64Value`](https://developers.google.com/discovery/v1/type-format)` format)` Total number of active workers. This does not correspond directly to slot usage. This is the largest value observed since the last sample.                                                  |
| `shuffleRamUsageRatio`   | `number` Total shuffle usage ratio in shuffle RAM per reservation of this query. This will be provided for reservation customers only.                                                                                                                                                  |
| `estimatedRunnableUnits` | `string ( `[`Int64Value`](https://developers.google.com/discovery/v1/type-format)` format)` Units of work that can be scheduled immediately. Providing additional slots for these units of work will accelerate the query, if no other query in the reservation needs additional slots. |

### ReservationResourceUsage

**JSON representation**

```
{
  "name": string,
  "slotMs": string
}
```

| Fields   |                                                                                                                                                                   |
|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`   | `string` Reservation name or "unreserved" for on-demand resource usage and multi-statement queries.                                                               |
| `slotMs` | `string ( `[`Int64Value`](https://developers.google.com/discovery/v1/type-format)` format)` Total slot milliseconds used by the reservation for a particular job. |

### RoutineReference

**JSON representation**

```
{
  "projectId": string,
  "datasetId": string,
  "routineId": string
}
```

| Fields      |                                                                                                                                                                  |
|-------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `projectId` | `string` Required. The ID of the project containing this routine.                                                                                                |
| `datasetId` | `string` Required. The ID of the dataset containing this routine.                                                                                                |
| `routineId` | `string` Required. The ID of the routine. The ID must contain only letters (a-z, A-Z), numbers (0-9), or underscores (\_). The maximum length is 256 characters. |

### PropertyGraphReference

**JSON representation**

```
{
  "projectId": string,
  "datasetId": string,
  "propertyGraphId": string
}
```

| Fields            |                                                                                                                                                                         |
|-------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `projectId`       | `string` Required. The ID of the project containing this property graph.                                                                                                |
| `datasetId`       | `string` Required. The ID of the dataset containing this property graph.                                                                                                |
| `propertyGraphId` | `string` Required. The ID of the property graph. The ID must contain only letters (a-z, A-Z), numbers (0-9), or underscores (\_). The maximum length is 256 characters. |

### DmlStats

**JSON representation**

```
{
  "insertedRowCount": string,
  "deletedRowCount": string,
  "updatedRowCount": string,
  "dmlMode": enum (DmlMode),
  "fineGrainedDmlUnusedReason": enum (FineGrainedDmlUnusedReason)
}
```

| Fields                       |                                                                                                                                                                                                                                         |
|------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `insertedRowCount`           | `string ( `[`Int64Value`](https://developers.google.com/discovery/v1/type-format)` format)` Output only. Number of inserted Rows. Populated by DML INSERT and MERGE statements                                                          |
| `deletedRowCount`            | `string ( `[`Int64Value`](https://developers.google.com/discovery/v1/type-format)` format)` Output only. Number of deleted Rows. populated by DML DELETE, MERGE and TRUNCATE statements.                                                |
| `updatedRowCount`            | `string ( `[`Int64Value`](https://developers.google.com/discovery/v1/type-format)` format)` Output only. Number of updated Rows. Populated by DML UPDATE and MERGE statements.                                                          |
| `dmlMode`                    | `enum ( `[`DmlMode`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.DmlMode)` )` Output only. DML mode used.                                                                             |
| `fineGrainedDmlUnusedReason` | `enum ( `[`FineGrainedDmlUnusedReason`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.FineGrainedDmlUnusedReason)` )` Output only. Reason for disabling fine-grained DML if applicable. |

### RowAccessPolicyReference

**JSON representation**

```
{
  "projectId": string,
  "datasetId": string,
  "tableId": string,
  "policyId": string
}
```

| Fields      |                                                                                                                                                                            |
|-------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `projectId` | `string` Required. The ID of the project containing this row access policy.                                                                                                |
| `datasetId` | `string` Required. The ID of the dataset containing this row access policy.                                                                                                |
| `tableId`   | `string` Required. The ID of the table containing this row access policy.                                                                                                  |
| `policyId`  | `string` Required. The ID of the row access policy. The ID must contain only letters (a-z, A-Z), numbers (0-9), or underscores (\_). The maximum length is 256 characters. |

### MlStatistics

**JSON representation**

```
{
  "maxIterations": string,
  "iterationResults": [
    {
      object (IterationResult)
    }
  ],
  "modelType": enum (ModelType),
  "trainingType": enum (TrainingType),
  "hparamTrials": [
    {
      object (HparamTuningTrial)
    }
  ]
}
```

| Fields               |                                                                                                                                                                                                                                                                                                                                         |
|----------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `maxIterations`      | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Output only. Maximum number of iterations specified as max_iterations in the 'CREATE MODEL' query. The actual number of iterations may be less than this number due to early stop.                                                               |
| `iterationResults[]` | `object ( `[`IterationResult`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.IterationResult)` )` Results for all completed iterations. Empty for [hyperparameter tuning jobs](https://cloud.google.com/bigquery-ml/docs/reference/standard-sql/bigqueryml-syntax-hp-tuning-overview) . |
| `modelType`          | `enum ( `[`ModelType`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.ModelType)` )` Output only. The type of the model that is being trained.                                                                                                                                           |
| `trainingType`       | `enum ( `[`TrainingType`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.TrainingType)` )` Output only. Training type of the job.                                                                                                                                                        |
| `hparamTrials[]`     | `object ( `[`HparamTuningTrial`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.HparamTuningTrial)` )` Output only. Trials of a [hyperparameter tuning job](https://cloud.google.com/bigquery-ml/docs/reference/standard-sql/bigqueryml-syntax-hp-tuning-overview) sorted by trial_id.   |

### IterationResult

**JSON representation**

```
{
  "index": integer,
  "durationMs": string,
  "trainingLoss": number,
  "evalLoss": number,
  "learnRate": number,
  "clusterInfos": [
    {
      object (ClusterInfo)
    }
  ],
  "arimaResult": {
    object (ArimaResult)
  },
  "principalComponentInfos": [
    {
      object (PrincipalComponentInfo)
    }
  ]
}
```

| Fields                      |                                                                                                                                                                                                              |
|-----------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `index`                     | `integer` Index of the iteration, 0 based.                                                                                                                                                                   |
| `durationMs`                | `string ( `[`Int64Value`](https://developers.google.com/discovery/v1/type-format)` format)` Time taken to run the iteration in milliseconds.                                                                 |
| `trainingLoss`              | `number` Loss computed on the training data at the end of iteration.                                                                                                                                         |
| `evalLoss`                  | `number` Loss computed on the eval data at the end of iteration.                                                                                                                                             |
| `learnRate`                 | `number` Learn rate used for this iteration.                                                                                                                                                                 |
| `clusterInfos[]`            | `object ( `[`ClusterInfo`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.ClusterInfo)` )` Information about top clusters for clustering models.              |
| `arimaResult`               | `object ( `[`ArimaResult`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.ArimaResult)` )` Arima result.                                                      |
| `principalComponentInfos[]` | `object ( `[`PrincipalComponentInfo`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.PrincipalComponentInfo)` )` The information of the principal components. |

### ClusterInfo

**JSON representation**

```
{
  "centroidId": string,
  "clusterRadius": number,
  "clusterSize": string
}
```

| Fields          |                                                                                                                                                               |
|-----------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `centroidId`    | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Centroid id.                                                           |
| `clusterRadius` | `number` Cluster radius, the average distance from centroid to each point assigned to the cluster.                                                            |
| `clusterSize`   | `string ( `[`Int64Value`](https://developers.google.com/discovery/v1/type-format)` format)` Cluster size, the total number of points assigned to the cluster. |

### ArimaResult

**JSON representation**

```
{
  "arimaModelInfo": [
    {
      object (ArimaModelInfo)
    }
  ],
  "seasonalPeriods": [
    enum (SeasonalPeriodType)
  ]
}
```

| Fields              |                                                                                                                                                                                                                                                                                   |
|---------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `arimaModelInfo[]`  | `object ( `[`ArimaModelInfo`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.ArimaModelInfo)` )` This message is repeated because there are multiple arima models fitted in auto-arima. For non-auto-arima model, its size is one. |
| `seasonalPeriods[]` | `enum ( `[`SeasonalPeriodType`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.SeasonalPeriodType)` )` Seasonal periods. Repeated because multiple periods are supported for one time series.                                      |

### ArimaModelInfo

**JSON representation**

```
{
  "nonSeasonalOrder": {
    object (ArimaOrder)
  },
  "arimaCoefficients": {
    object (ArimaCoefficients)
  },
  "arimaFittingMetrics": {
    object (ArimaFittingMetrics)
  },
  "hasDrift": boolean,
  "timeSeriesId": string,
  "timeSeriesIds": [
    string
  ],
  "seasonalPeriods": [
    enum (SeasonalPeriodType)
  ],
  "hasHolidayEffect": boolean,
  "hasSpikesAndDips": boolean,
  "hasStepChanges": boolean
}
```

| Fields                |                                                                                                                                                                                                                                                                                                                                                |
|-----------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `nonSeasonalOrder`    | `object ( `[`ArimaOrder`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.ArimaOrder)` )` Non-seasonal order.                                                                                                                                                                                    |
| `arimaCoefficients`   | `object ( `[`ArimaCoefficients`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.ArimaCoefficients)` )` Arima coefficients.                                                                                                                                                                      |
| `arimaFittingMetrics` | `object ( `[`ArimaFittingMetrics`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.ArimaFittingMetrics)` )` Arima fitting metrics.                                                                                                                                                               |
| `hasDrift`            | `boolean` Whether Arima model fitted with drift or not. It is always false when d is not 1.                                                                                                                                                                                                                                                    |
| `timeSeriesId`        | `string` The time_series_id value for this time series. It will be one of the unique values from the time_series_id_column specified during ARIMA model training. Only present when time_series_id_column training option was used.                                                                                                            |
| `timeSeriesIds[]`     | `string` The tuple of time_series_ids identifying this time series. It will be one of the unique tuples of values present in the time_series_id_columns specified during ARIMA model training. Only present when time_series_id_columns training option was used and the order of values here are same as the order of time_series_id_columns. |
| `seasonalPeriods[]`   | `enum ( `[`SeasonalPeriodType`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.SeasonalPeriodType)` )` Seasonal periods. Repeated because multiple periods are supported for one time series.                                                                                                   |
| `hasHolidayEffect`    | `boolean` If true, holiday_effect is a part of time series decomposition result.                                                                                                                                                                                                                                                               |
| `hasSpikesAndDips`    | `boolean` If true, spikes_and_dips is a part of time series decomposition result.                                                                                                                                                                                                                                                              |
| `hasStepChanges`      | `boolean` If true, step_changes is a part of time series decomposition result.                                                                                                                                                                                                                                                                 |

### ArimaOrder

**JSON representation**

```
{
  "p": string,
  "d": string,
  "q": string
}
```

| Fields |                                                                                                                               |
|--------|-------------------------------------------------------------------------------------------------------------------------------|
| `p`    | `string ( `[`Int64Value`](https://developers.google.com/discovery/v1/type-format)` format)` Order of the autoregressive part. |
| `d`    | `string ( `[`Int64Value`](https://developers.google.com/discovery/v1/type-format)` format)` Order of the differencing part.   |
| `q`    | `string ( `[`Int64Value`](https://developers.google.com/discovery/v1/type-format)` format)` Order of the moving-average part. |

### ArimaCoefficients

**JSON representation**

```
{
  "autoRegressiveCoefficients": [
    number
  ],
  "movingAverageCoefficients": [
    number
  ],
  "interceptCoefficient": number
}
```

| Fields                         |                                                             |
|--------------------------------|-------------------------------------------------------------|
| `autoRegressiveCoefficients[]` | `number` Auto-regressive coefficients, an array of double.  |
| `movingAverageCoefficients[]`  | `number` Moving-average coefficients, an array of double.   |
| `interceptCoefficient`         | `number` Intercept coefficient, just a double not an array. |

### ArimaFittingMetrics

**JSON representation**

```
{
  "logLikelihood": number,
  "aic": number,
  "variance": number
}
```

| Fields          |                          |
|-----------------|--------------------------|
| `logLikelihood` | `number` Log-likelihood. |
| `aic`           | `number` AIC.            |
| `variance`      | `number` Variance.       |

### PrincipalComponentInfo

**JSON representation**

```
{
  "principalComponentId": string,
  "explainedVariance": number,
  "explainedVarianceRatio": number,
  "cumulativeExplainedVarianceRatio": number
}
```

| Fields                             |                                                                                                                            |
|------------------------------------|----------------------------------------------------------------------------------------------------------------------------|
| `principalComponentId`             | `string ( `[`Int64Value`](https://developers.google.com/discovery/v1/type-format)` format)` Id of the principal component. |
| `explainedVariance`                | `number` Explained variance by this principal component, which is simply the eigenvalue.                                   |
| `explainedVarianceRatio`           | `number` Explained_variance over the total explained variance.                                                             |
| `cumulativeExplainedVarianceRatio` | `number` The explained_variance is pre-ordered in the descending order to compute the cumulative explained variance ratio. |

### HparamTuningTrial

**JSON representation**

```
{
  "trialId": string,
  "startTimeMs": string,
  "endTimeMs": string,
  "hparams": {
    object (TrainingOptions)
  },
  "evaluationMetrics": {
    object (EvaluationMetrics)
  },
  "status": enum (TrialStatus),
  "errorMessage": string,
  "trainingLoss": number,
  "evalLoss": number,
  "hparamTuningEvaluationMetrics": {
    object (EvaluationMetrics)
  }
}
```

| Fields                          |                                                                                                                                                                                                                                                                                                                                             |
|---------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `trialId`                       | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` 1-based index of the trial.                                                                                                                                                                                                                          |
| `startTimeMs`                   | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Starting time of the trial.                                                                                                                                                                                                                          |
| `endTimeMs`                     | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Ending time of the trial.                                                                                                                                                                                                                            |
| `hparams`                       | `object ( `[`TrainingOptions`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.TrainingOptions)` )` The hyperprameters selected for this trial.                                                                                                                                               |
| `evaluationMetrics`             | `object ( `[`EvaluationMetrics`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.EvaluationMetrics)` )` Evaluation metrics of this trial calculated on the test data. Empty in Job API.                                                                                                       |
| `status`                        | `enum ( `[`TrialStatus`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.TrialStatus)` )` The status of the trial.                                                                                                                                                                            |
| `errorMessage`                  | `string` Error message for FAILED and INFEASIBLE trial.                                                                                                                                                                                                                                                                                     |
| `trainingLoss`                  | `number` Loss computed on the training data at the end of trial.                                                                                                                                                                                                                                                                            |
| `evalLoss`                      | `number` Loss computed on the eval data at the end of trial.                                                                                                                                                                                                                                                                                |
| `hparamTuningEvaluationMetrics` | `object ( `[`EvaluationMetrics`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.EvaluationMetrics)` )` Hyperparameter tuning evaluation metrics of this trial calculated on the eval data. Unlike evaluation_metrics, only the fields corresponding to the hparam_tuning_objectives are set. |

### TrainingOptions

**JSON representation**

```
{
  "maxIterations": string,
  "lossType": enum (LossType),
  "learnRate": number,
  "l1Regularization": number,
  "l2Regularization": number,
  "minRelativeProgress": number,
  "warmStart": boolean,
  "earlyStop": boolean,
  "inputLabelColumns": [
    string
  ],
  "dataSplitMethod": enum (DataSplitMethod),
  "dataSplitEvalFraction": number,
  "dataSplitColumn": string,
  "learnRateStrategy": enum (LearnRateStrategy),
  "initialLearnRate": number,
  "labelClassWeights": {
    string: number,
    ...
  },
  "userColumn": string,
  "itemColumn": string,
  "distanceType": enum (DistanceType),
  "numClusters": string,
  "modelUri": string,
  "optimizationStrategy": enum (OptimizationStrategy),
  "hiddenUnits": [
    string
  ],
  "batchSize": string,
  "dropout": number,
  "maxTreeDepth": string,
  "subsample": number,
  "minSplitLoss": number,
  "boosterType": enum (BoosterType),
  "numParallelTree": string,
  "dartNormalizeType": enum (DartNormalizeType),
  "treeMethod": enum (TreeMethod),
  "minTreeChildWeight": string,
  "colsampleBytree": number,
  "colsampleBylevel": number,
  "colsampleBynode": number,
  "numFactors": string,
  "feedbackType": enum (FeedbackType),
  "walsAlpha": number,
  "kmeansInitializationMethod": enum (KmeansInitializationMethod),
  "kmeansInitializationColumn": string,
  "timeSeriesTimestampColumn": string,
  "timeSeriesDataColumn": string,
  "autoArima": boolean,
  "nonSeasonalOrder": {
    object (ArimaOrder)
  },
  "dataFrequency": enum (DataFrequency),
  "calculatePValues": boolean,
  "includeDrift": boolean,
  "holidayRegion": enum (HolidayRegion),
  "holidayRegions": [
    enum (HolidayRegion)
  ],
  "timeSeriesIdColumn": string,
  "timeSeriesIdColumns": [
    string
  ],
  "forecastLimitLowerBound": number,
  "forecastLimitUpperBound": number,
  "horizon": string,
  "autoArimaMaxOrder": string,
  "autoArimaMinOrder": string,
  "numTrials": string,
  "maxParallelTrials": string,
  "hparamTuningObjectives": [
    enum (HparamTuningObjective)
  ],
  "decomposeTimeSeries": boolean,
  "cleanSpikesAndDips": boolean,
  "adjustStepChanges": boolean,
  "enableGlobalExplain": boolean,
  "sampledShapleyNumPaths": string,
  "integratedGradientsNumSteps": string,
  "categoryEncodingMethod": enum (EncodingMethod),
  "tfVersion": string,
  "colorSpace": enum (ColorSpace),
  "instanceWeightColumn": string,
  "trendSmoothingWindowSize": string,
  "timeSeriesLengthFraction": number,
  "minTimeSeriesLength": string,
  "maxTimeSeriesLength": string,
  "xgboostVersion": string,
  "approxGlobalFeatureContrib": boolean,
  "fitIntercept": boolean,
  "numPrincipalComponents": string,
  "pcaExplainedVarianceRatio": number,
  "scaleFeatures": boolean,
  "pcaSolver": enum (PcaSolver),
  "autoClassWeights": boolean,
  "activationFn": string,
  "optimizer": string,
  "budgetHours": number,
  "standardizeFeatures": boolean,
  "l1RegActivation": number,
  "modelRegistry": enum (ModelRegistry),
  "vertexAiModelVersionAliases": [
    string
  ],
  "dimensionIdColumns": [
    string
  ],
  "reservationAffinityValues": [
    string
  ],

  // Union field _contribution_metric can be only one of the following:
  "contributionMetric": string
  // End of list of possible types for union field _contribution_metric.

  // Union field _is_test_column can be only one of the following:
  "isTestColumn": string
  // End of list of possible types for union field _is_test_column.

  // Union field _min_apriori_support can be only one of the following:
  "minAprioriSupport": number
  // End of list of possible types for union field _min_apriori_support.

  // Union field external_model_id can be only one of the following:
  "huggingFaceModelId": string,
  "modelGardenModelName": string
  // End of list of possible types for union field external_model_id.

  // Union field _endpoint_idle_ttl can be only one of the following:
  "endpointIdleTtl": string
  // End of list of possible types for union field _endpoint_idle_ttl.

  // Union field _machine_type can be only one of the following:
  "machineType": string
  // End of list of possible types for union field _machine_type.

  // Union field _min_replica_count can be only one of the following:
  "minReplicaCount": string
  // End of list of possible types for union field _min_replica_count.

  // Union field _max_replica_count can be only one of the following:
  "maxReplicaCount": string
  // End of list of possible types for union field _max_replica_count.

  // Union field _reservation_affinity_type can be only one of the following:
  "reservationAffinityType": enum (ReservationAffinityType)
  // End of list of possible types for union field _reservation_affinity_type.

  // Union field _reservation_affinity_key can be only one of the following:
  "reservationAffinityKey": string
  // End of list of possible types for union field _reservation_affinity_key.
}
```

| Fields                                                                                                                                     |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
|--------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `maxIterations`                                                                                                                            | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` The maximum number of iterations in training. Used only for iterative training algorithms.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| `lossType`                                                                                                                                 | `enum ( `[`LossType`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.LossType)` )` Type of loss function used during training run.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| `learnRate`                                                                                                                                | `number` Learning rate in training. Used only for iterative training algorithms.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| `l1Regularization`                                                                                                                         | `number` L1 regularization coefficient.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `l2Regularization`                                                                                                                         | `number` L2 regularization coefficient.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `minRelativeProgress`                                                                                                                      | `number` When early_stop is true, stops training when accuracy improvement is less than 'min_relative_progress'. Used only for iterative training algorithms.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| `warmStart`                                                                                                                                | `boolean` Whether to train a model from the last checkpoint.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| `earlyStop`                                                                                                                                | `boolean` Whether to stop early when the loss doesn't improve significantly any more (compared to min_relative_progress). Used only for iterative training algorithms.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `inputLabelColumns[]`                                                                                                                      | `string` Name of input label columns in training data.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `dataSplitMethod`                                                                                                                          | `enum ( `[`DataSplitMethod`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.DataSplitMethod)` )` The data split type for training and evaluation, e.g. RANDOM.                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| `dataSplitEvalFraction`                                                                                                                    | `number` The fraction of evaluation data over the whole input data. The rest of data will be used as training data. The format should be double. Accurate to two decimal places. Default value is 0.2.                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `dataSplitColumn`                                                                                                                          | `string` The column to split data with. This column won't be used as a feature. 1. When data_split_method is CUSTOM, the corresponding column should be boolean. The rows with true value tag are eval data, and the false are training data. 2. When data_split_method is SEQ, the first DATA_SPLIT_EVAL_FRACTION rows (from smallest to largest) in the corresponding column are used as training data, and the rest are eval data. It respects the order in Orderable data types: <https://cloud.google.com/bigquery/docs/reference/standard-sql/data-types#data_type_properties>                                                                                          |
| `learnRateStrategy`                                                                                                                        | `enum ( `[`LearnRateStrategy`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.LearnRateStrategy)` )` The strategy to determine learn rate for the current iteration.                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| `initialLearnRate`                                                                                                                         | `number` Specifies the initial learning rate for the line search learn rate strategy.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| `labelClassWeights`                                                                                                                        | `map (key: string, value: number)` Weights associated with each label class, for rebalancing the training data. Only applicable for classification models. An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .                                                                                                                                                                                                                                                                                                                                                                                              |
| `userColumn`                                                                                                                               | `string` User column specified for matrix factorization models.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| `itemColumn`                                                                                                                               | `string` Item column specified for matrix factorization models.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| `distanceType`                                                                                                                             | `enum ( `[`DistanceType`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.DistanceType)` )` Distance type for clustering models.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| `numClusters`                                                                                                                              | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Number of clusters for clustering models.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| `modelUri`                                                                                                                                 | `string` Google Cloud Storage URI from which the model was imported. Only applicable for imported models.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| `optimizationStrategy`                                                                                                                     | `enum ( `[`OptimizationStrategy`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.OptimizationStrategy)` )` Optimization strategy for training linear regression models.                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `hiddenUnits[]`                                                                                                                            | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Hidden units for dnn models.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| `batchSize`                                                                                                                                | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Batch size for dnn models.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| `dropout`                                                                                                                                  | `number` Dropout probability for dnn models.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| `maxTreeDepth`                                                                                                                             | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Maximum depth of a tree for boosted tree models.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `subsample`                                                                                                                                | `number` Subsample fraction of the training data to grow tree to prevent overfitting for boosted tree models.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| `minSplitLoss`                                                                                                                             | `number` Minimum split loss for boosted tree models.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| `boosterType`                                                                                                                              | `enum ( `[`BoosterType`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.BoosterType)` )` Booster type for boosted tree models.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| `numParallelTree`                                                                                                                          | `string ( `[`Int64Value`](https://developers.google.com/discovery/v1/type-format)` format)` Number of parallel trees constructed during each iteration for boosted tree models.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| `dartNormalizeType`                                                                                                                        | `enum ( `[`DartNormalizeType`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.DartNormalizeType)` )` Type of normalization algorithm for boosted tree models using dart booster.                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| `treeMethod`                                                                                                                               | `enum ( `[`TreeMethod`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.TreeMethod)` )` Tree construction algorithm for boosted tree models.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| `minTreeChildWeight`                                                                                                                       | `string ( `[`Int64Value`](https://developers.google.com/discovery/v1/type-format)` format)` Minimum sum of instance weight needed in a child for boosted tree models.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| `colsampleBytree`                                                                                                                          | `number` Subsample ratio of columns when constructing each tree for boosted tree models.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| `colsampleBylevel`                                                                                                                         | `number` Subsample ratio of columns for each level for boosted tree models.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| `colsampleBynode`                                                                                                                          | `number` Subsample ratio of columns for each node(split) for boosted tree models.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| `numFactors`                                                                                                                               | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Num factors specified for matrix factorization models.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| `feedbackType`                                                                                                                             | `enum ( `[`FeedbackType`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.FeedbackType)` )` Feedback type that specifies which algorithm to run for matrix factorization.                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `walsAlpha`                                                                                                                                | `number` Hyperparameter for matrix factoration when implicit feedback type is specified.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| `kmeansInitializationMethod`                                                                                                               | `enum ( `[`KmeansInitializationMethod`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.KmeansInitializationMethod)` )` The method used to initialize the centroids for kmeans algorithm.                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `kmeansInitializationColumn`                                                                                                               | `string` The column used to provide the initial centroids for kmeans algorithm when kmeans_initialization_method is CUSTOM.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| `timeSeriesTimestampColumn`                                                                                                                | `string` Column to be designated as time series timestamp for ARIMA model.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| `timeSeriesDataColumn`                                                                                                                     | `string` Column to be designated as time series data for ARIMA model.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| `autoArima`                                                                                                                                | `boolean` Whether to enable auto ARIMA or not.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| `nonSeasonalOrder`                                                                                                                         | `object ( `[`ArimaOrder`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.ArimaOrder)` )` A specification of the non-seasonal part of the ARIMA model: the three components (p, d, q) are the AR order, the degree of differencing, and the MA order.                                                                                                                                                                                                                                                                                                                                                                           |
| `dataFrequency`                                                                                                                            | `enum ( `[`DataFrequency`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.DataFrequency)` )` The data frequency of a time series.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| `calculatePValues`                                                                                                                         | `boolean` Whether or not p-value test should be computed for this model. Only available for linear and logistic regression models.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| `includeDrift`                                                                                                                             | `boolean` Include drift when fitting an ARIMA model.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| `holidayRegion`                                                                                                                            | `enum ( `[`HolidayRegion`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.HolidayRegion)` )` The geographical region based on which the holidays are considered in time series modeling. If a valid value is specified, then holiday effects modeling is enabled.                                                                                                                                                                                                                                                                                                                                                              |
| `holidayRegions[]`                                                                                                                         | `enum ( `[`HolidayRegion`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.HolidayRegion)` )` A list of geographical regions that are used for time series modeling.                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| `timeSeriesIdColumn`                                                                                                                       | `string` The time series id column that was used during ARIMA model training.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| `timeSeriesIdColumns[]`                                                                                                                    | `string` The time series id columns that were used during ARIMA model training.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| `forecastLimitLowerBound`                                                                                                                  | `number` The forecast limit lower bound that was used during ARIMA model training with limits. To see more details of the algorithm: <https://otexts.com/fpp2/limits.html>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| `forecastLimitUpperBound`                                                                                                                  | `number` The forecast limit upper bound that was used during ARIMA model training with limits.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| `horizon`                                                                                                                                  | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` The number of periods ahead that need to be forecasted.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| `autoArimaMaxOrder`                                                                                                                        | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` The max value of the sum of non-seasonal p and q.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| `autoArimaMinOrder`                                                                                                                        | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` The min value of the sum of non-seasonal p and q.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| `numTrials`                                                                                                                                | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Number of trials to run this hyperparameter tuning job.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| `maxParallelTrials`                                                                                                                        | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Maximum number of trials to run in parallel.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| `hparamTuningObjectives[]`                                                                                                                 | `enum ( `[`HparamTuningObjective`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.HparamTuningObjective)` )` The target evaluation metrics to optimize the hyperparameters for.                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| `decomposeTimeSeries`                                                                                                                      | `boolean` If true, perform decompose time series and save the results.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `cleanSpikesAndDips`                                                                                                                       | `boolean` If true, clean spikes and dips in the input time series.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| `adjustStepChanges`                                                                                                                        | `boolean` If true, detect step changes and make data adjustment in the input time series.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| `enableGlobalExplain`                                                                                                                      | `boolean` If true, enable global explanation during training.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| `sampledShapleyNumPaths`                                                                                                                   | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Number of paths for the sampled Shapley explain method.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| `integratedGradientsNumSteps`                                                                                                              | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Number of integral steps for the integrated gradients explain method.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| `categoryEncodingMethod`                                                                                                                   | `enum ( `[`EncodingMethod`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.EncodingMethod)` )` Categorical feature encoding method.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| `tfVersion`                                                                                                                                | `string` Based on the selected TF version, the corresponding docker image is used to train external models.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| `colorSpace`                                                                                                                               | `enum ( `[`ColorSpace`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.ColorSpace)` )` Enums for color space, used for processing images in Object Table. See more details at <https://www.tensorflow.org/io/tutorials/colorspace> .                                                                                                                                                                                                                                                                                                                                                                                           |
| `instanceWeightColumn`                                                                                                                     | `string` Name of the instance weight column for training data. This column isn't be used as a feature.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `trendSmoothingWindowSize`                                                                                                                 | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Smoothing window size for the trend component. When a positive value is specified, a center moving average smoothing is applied on the history trend. When the smoothing window is out of the boundary at the beginning or the end of the trend, the first element or the last element is padded to fill the smoothing window before the average is applied.                                                                                                                                                                                                                           |
| `timeSeriesLengthFraction`                                                                                                                 | `number` The fraction of the interpolated length of the time series that's used to model the time series trend component. All of the time points of the time series are used to model the non-trend component. This training option accelerates modeling training without sacrificing much forecasting accuracy. You can use this option with `minTimeSeriesLength` but not with `maxTimeSeriesLength` .                                                                                                                                                                                                                                                                      |
| `minTimeSeriesLength`                                                                                                                      | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` The minimum number of time points in a time series that are used in modeling the trend component of the time series. If you use this option you must also set the `timeSeriesLengthFraction` option. This training option ensures that enough time points are available when you use `timeSeriesLengthFraction` in trend modeling. This is particularly important when forecasting multiple time series in a single query using `timeSeriesIdColumn` . If the total number of time points is less than the `minTimeSeriesLength` value, then the query uses all available time points. |
| `maxTimeSeriesLength`                                                                                                                      | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` The maximum number of time points in a time series that can be used in modeling the trend component of the time series. Don't use this option with the `timeSeriesLengthFraction` or `minTimeSeriesLength` options.                                                                                                                                                                                                                                                                                                                                                                    |
| `xgboostVersion`                                                                                                                           | `string` User-selected XGBoost versions for training of XGBoost models.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `approxGlobalFeatureContrib`                                                                                                               | `boolean` Whether to use approximate feature contribution method in XGBoost model explanation for global explain.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| `fitIntercept`                                                                                                                             | `boolean` Whether the model should include intercept during model training.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| `numPrincipalComponents`                                                                                                                   | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Number of principal components to keep in the PCA model. Must be \<= the number of features.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| `pcaExplainedVarianceRatio`                                                                                                                | `number` The minimum ratio of cumulative explained variance that needs to be given by the PCA model.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| `scaleFeatures`                                                                                                                            | `boolean` If true, scale the feature values by dividing the feature standard deviation. Currently only apply to PCA.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| `pcaSolver`                                                                                                                                | `enum ( `[`PcaSolver`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.PcaSolver)` )` The solver for PCA.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `autoClassWeights`                                                                                                                         | `boolean` Whether to calculate class weights automatically based on the popularity of each label.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| `activationFn`                                                                                                                             | `string` Activation function of the neural nets.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| `optimizer`                                                                                                                                | `string` Optimizer used for training the neural nets.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| `budgetHours`                                                                                                                              | `number` Budget in hours for AutoML training.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| `standardizeFeatures`                                                                                                                      | `boolean` Whether to standardize numerical features. Default to true.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| `l1RegActivation`                                                                                                                          | `number` L1 regularization coefficient to activations.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `modelRegistry`                                                                                                                            | `enum ( `[`ModelRegistry`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.ModelRegistry)` )` The model registry.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| `vertexAiModelVersionAliases[]`                                                                                                            | `string` The version aliases to apply in Vertex AI model registry. Always overwrite if the version aliases exists in a existing model.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `dimensionIdColumns[]`                                                                                                                     | `string` Optional. Names of the columns to slice on. Applies to contribution analysis models.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| `reservationAffinityValues[]`                                                                                                              | `string` Corresponds to the label values of a reservation resource used by Vertex AI. This must be the full resource name of the reservation or reservation block.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| Union field `_contribution_metric` . `_contribution_metric` can be only one of the following:                                              |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| `contributionMetric`                                                                                                                       | `string` The contribution metric. Applies to contribution analysis models. Allowed formats supported are for summable and summable ratio contribution metrics. These include expressions such as `SUM(x)` or `SUM(x)/SUM(y)` , where x and y are column names from the base table.                                                                                                                                                                                                                                                                                                                                                                                            |
|                                                                                                                                            |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| Union field `_is_test_column` . `_is_test_column` can be only one of the following:                                                        |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| `isTestColumn`                                                                                                                             | `string` Name of the column used to determine the rows corresponding to control and test. Applies to contribution analysis models.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
|                                                                                                                                            |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| Union field `_min_apriori_support` . `_min_apriori_support` can be only one of the following:                                              |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| `minAprioriSupport`                                                                                                                        | `number` The apriori support minimum. Applies to contribution analysis models.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
|                                                                                                                                            |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| Union field `external_model_id` . The id that uniquely identifies an external model. `external_model_id` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| `huggingFaceModelId`                                                                                                                       | `string` The id of a Hugging Face model. For example, `google/gemma-2-2b-it` .                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| `modelGardenModelName`                                                                                                                     | `string` The name of a Vertex model garden publisher model. Format is `publishers/{publisher}/models/{model}@{optional_version_id}` .                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
|                                                                                                                                            |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| Union field `_endpoint_idle_ttl` . `_endpoint_idle_ttl` can be only one of the following:                                                  |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| `endpointIdleTtl`                                                                                                                          | `string ( `[`Duration`](https://protobuf.dev/reference/protobuf/google.protobuf/#duration)` format)` The idle TTL of the endpoint before the resources get destroyed. The default value is 6.5 hours. A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .                                                                                                                                                                                                                                                                                                                                                                       |
|                                                                                                                                            |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| Union field `_machine_type` . `_machine_type` can be only one of the following:                                                            |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| `machineType`                                                                                                                              | `string` The type of the machine used to deploy and serve the model.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
|                                                                                                                                            |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| Union field `_min_replica_count` . `_min_replica_count` can be only one of the following:                                                  |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| `minReplicaCount`                                                                                                                          | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` The minimum number of machine replicas that will be always deployed on an endpoint. This value must be greater than or equal to 1. The default value is 1.                                                                                                                                                                                                                                                                                                                                                                                                                             |
|                                                                                                                                            |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| Union field `_max_replica_count` . `_max_replica_count` can be only one of the following:                                                  |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| `maxReplicaCount`                                                                                                                          | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` The maximum number of machine replicas that will be deployed on an endpoint. The default value is equal to min_replica_count.                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
|                                                                                                                                            |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| Union field `_reservation_affinity_type` . `_reservation_affinity_type` can be only one of the following:                                  |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| `reservationAffinityType`                                                                                                                  | `enum ( `[`ReservationAffinityType`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.ReservationAffinityType)` )` Specifies the reservation affinity type used to configure a Vertex AI resource. The default value is `NO_RESERVATION` .                                                                                                                                                                                                                                                                                                                                                                                       |
|                                                                                                                                            |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| Union field `_reservation_affinity_key` . `_reservation_affinity_key` can be only one of the following:                                    |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| `reservationAffinityKey`                                                                                                                   | `string` Corresponds to the label key of a reservation resource used by Vertex AI. To target a SPECIFIC_RESERVATION by name, use `compute.googleapis.com/reservation-name` as the key and specify the name of your reservation as its value.                                                                                                                                                                                                                                                                                                                                                                                                                                  |
|                                                                                                                                            |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |

### LabelClassWeightsEntry

**JSON representation**

```
{
  "key": string,
  "value": number
}
```

| Fields  |          |
|---------|----------|
| `key`   | `string` |
| `value` | `number` |

### Duration

**JSON representation**

```
{
  "seconds": string,
  "nanos": integer
}
```

| Fields    |                                                                                                                                                                                                                                                                                                                                                                                          |
|-----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `seconds` | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Signed seconds of the span of time. Must be from -315,576,000,000 to +315,576,000,000 inclusive. Note: these bounds are computed from: 60 sec/min \* 60 min/hr \* 24 hr/day \* 365.25 days/year \* 10000 years                                                                                    |
| `nanos`   | `integer` Signed fractions of a second at nanosecond resolution of the span of time. Durations less than one second are represented with a 0 `seconds` field and a positive or negative `nanos` field. For durations of one second or more, a non-zero value for the `nanos` field must be of the same sign as the `seconds` field. Must be from -999,999,999 to +999,999,999 inclusive. |

### EvaluationMetrics

**JSON representation**

```
{

  // Union field metrics can be only one of the following:
  "regressionMetrics": {
    object (RegressionMetrics)
  },
  "binaryClassificationMetrics": {
    object (BinaryClassificationMetrics)
  },
  "multiClassClassificationMetrics": {
    object (MultiClassClassificationMetrics)
  },
  "clusteringMetrics": {
    object (ClusteringMetrics)
  },
  "rankingMetrics": {
    object (RankingMetrics)
  },
  "arimaForecastingMetrics": {
    object (ArimaForecastingMetrics)
  },
  "dimensionalityReductionMetrics": {
    object (DimensionalityReductionMetrics)
  }
  // End of list of possible types for union field metrics.
}
```

| Fields                                                                       |                                                                                                                                                                                                                                                                                      |
|------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `metrics` . Metrics. `metrics` can be only one of the following: |                                                                                                                                                                                                                                                                                      |
| `regressionMetrics`                                                          | `object ( `[`RegressionMetrics`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.RegressionMetrics)` )` Populated for regression models and explicit feedback type matrix factorization models.                                        |
| `binaryClassificationMetrics`                                                | `object ( `[`BinaryClassificationMetrics`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.BinaryClassificationMetrics)` )` Populated for binary classification/classifier models.                                                     |
| `multiClassClassificationMetrics`                                            | `object ( `[`MultiClassClassificationMetrics`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.MultiClassClassificationMetrics)` )` Populated for multi-class classification/classifier models.                                        |
| `clusteringMetrics`                                                          | `object ( `[`ClusteringMetrics`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.ClusteringMetrics)` )` Populated for clustering models.                                                                                               |
| `rankingMetrics`                                                             | `object ( `[`RankingMetrics`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.RankingMetrics)` )` Populated for implicit feedback type matrix factorization models.                                                                    |
| `arimaForecastingMetrics`                                                    | `object ( `[`ArimaForecastingMetrics`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.ArimaForecastingMetrics)` )` Populated for ARIMA models.                                                                                        |
| `dimensionalityReductionMetrics`                                             | `object ( `[`DimensionalityReductionMetrics`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.DimensionalityReductionMetrics)` )` Evaluation metrics when the model is a dimensionality reduction model, which currently includes PCA. |
|                                                                              |                                                                                                                                                                                                                                                                                      |

### RegressionMetrics

**JSON representation**

```
{
  "meanAbsoluteError": number,
  "meanSquaredError": number,
  "meanSquaredLogError": number,
  "medianAbsoluteError": number,
  "rSquared": number
}
```

| Fields                |                                                                  |
|-----------------------|------------------------------------------------------------------|
| `meanAbsoluteError`   | `number` Mean absolute error.                                    |
| `meanSquaredError`    | `number` Mean squared error.                                     |
| `meanSquaredLogError` | `number` Mean squared log error.                                 |
| `medianAbsoluteError` | `number` Median absolute error.                                  |
| `rSquared`            | `number` R^2 score. This corresponds to r2_score in ML.EVALUATE. |

### BinaryClassificationMetrics

**JSON representation**

```
{
  "aggregateClassificationMetrics": {
    object (AggregateClassificationMetrics)
  },
  "binaryConfusionMatrixList": [
    {
      object (BinaryConfusionMatrix)
    }
  ],
  "positiveLabel": string,
  "negativeLabel": string
}
```

| Fields                           |                                                                                                                                                                                                                   |
|----------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `aggregateClassificationMetrics` | `object ( `[`AggregateClassificationMetrics`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.AggregateClassificationMetrics)` )` Aggregate classification metrics. |
| `binaryConfusionMatrixList[]`    | `object ( `[`BinaryConfusionMatrix`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.BinaryConfusionMatrix)` )` Binary confusion matrix at multiple thresholds.     |
| `positiveLabel`                  | `string` Label representing the positive class.                                                                                                                                                                   |
| `negativeLabel`                  | `string` Label representing the negative class.                                                                                                                                                                   |

### AggregateClassificationMetrics

**JSON representation**

```
{
  "precision": number,
  "recall": number,
  "accuracy": number,
  "threshold": number,
  "f1Score": number,
  "logLoss": number,
  "rocAuc": number
}
```

| Fields      |                                                                                                                                                                                                      |
|-------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `precision` | `number` Precision is the fraction of actual positive predictions that had positive actual labels. For multiclass this is a macro-averaged metric treating each class as a binary classifier.        |
| `recall`    | `number` Recall is the fraction of actual positive labels that were given a positive prediction. For multiclass this is a macro-averaged metric.                                                     |
| `accuracy`  | `number` Accuracy is the fraction of predictions given the correct label. For multiclass this is a micro-averaged metric.                                                                            |
| `threshold` | `number` Threshold at which the metrics are computed. For binary classification models this is the positive class threshold. For multi-class classification models this is the confidence threshold. |
| `f1Score`   | `number` The F1 score is an average of recall and precision. For multiclass this is a macro-averaged metric.                                                                                         |
| `logLoss`   | `number` Logarithmic Loss. For multiclass this is a macro-averaged metric.                                                                                                                           |
| `rocAuc`    | `number` Area Under a ROC Curve. For multiclass this is a macro-averaged metric.                                                                                                                     |

### BinaryConfusionMatrix

**JSON representation**

```
{
  "positiveClassThreshold": number,
  "truePositives": string,
  "falsePositives": string,
  "trueNegatives": string,
  "falseNegatives": string,
  "precision": number,
  "recall": number,
  "f1Score": number,
  "accuracy": number
}
```

| Fields                   |                                                                                                                                         |
|--------------------------|-----------------------------------------------------------------------------------------------------------------------------------------|
| `positiveClassThreshold` | `number` Threshold value used when computing each of the following metric.                                                              |
| `truePositives`          | `string ( `[`Int64Value`](https://developers.google.com/discovery/v1/type-format)` format)` Number of true samples predicted as true.   |
| `falsePositives`         | `string ( `[`Int64Value`](https://developers.google.com/discovery/v1/type-format)` format)` Number of false samples predicted as true.  |
| `trueNegatives`          | `string ( `[`Int64Value`](https://developers.google.com/discovery/v1/type-format)` format)` Number of true samples predicted as false.  |
| `falseNegatives`         | `string ( `[`Int64Value`](https://developers.google.com/discovery/v1/type-format)` format)` Number of false samples predicted as false. |
| `precision`              | `number` The fraction of actual positive predictions that had positive actual labels.                                                   |
| `recall`                 | `number` The fraction of actual positive labels that were given a positive prediction.                                                  |
| `f1Score`                | `number` The equally weighted average of recall and precision.                                                                          |
| `accuracy`               | `number` The fraction of predictions given the correct label.                                                                           |

### MultiClassClassificationMetrics

**JSON representation**

```
{
  "aggregateClassificationMetrics": {
    object (AggregateClassificationMetrics)
  },
  "confusionMatrixList": [
    {
      object (ConfusionMatrix)
    }
  ]
}
```

| Fields                           |                                                                                                                                                                                                                   |
|----------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `aggregateClassificationMetrics` | `object ( `[`AggregateClassificationMetrics`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.AggregateClassificationMetrics)` )` Aggregate classification metrics. |
| `confusionMatrixList[]`          | `object ( `[`ConfusionMatrix`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.ConfusionMatrix)` )` Confusion matrix at different thresholds.                       |

### ConfusionMatrix

**JSON representation**

```
{
  "confidenceThreshold": number,
  "rows": [
    {
      object (Row)
    }
  ]
}
```

| Fields                |                                                                                                                                                     |
|-----------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------|
| `confidenceThreshold` | `number` Confidence threshold used when computing the entries of the confusion matrix.                                                              |
| `rows[]`              | `object ( `[`Row`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.Row)` )` One row per actual label. |

### Row

**JSON representation**

```
{
  "actualLabel": string,
  "entries": [
    {
      object (Entry)
    }
  ]
}
```

| Fields        |                                                                                                                                                                             |
|---------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `actualLabel` | `string` The original label of this row.                                                                                                                                    |
| `entries[]`   | `object ( `[`Entry`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.Entry)` )` Info describing predicted label distribution. |

### Entry

**JSON representation**

```
{
  "predictedLabel": string,
  "itemCount": string
}
```

| Fields           |                                                                                                                                                       |
|------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
| `predictedLabel` | `string` The predicted label. For confidence_threshold \> 0, we will also add an entry indicating the number of items under the confidence threshold. |
| `itemCount`      | `string ( `[`Int64Value`](https://developers.google.com/discovery/v1/type-format)` format)` Number of items being predicted as this label.            |

### ClusteringMetrics

**JSON representation**

```
{
  "daviesBouldinIndex": number,
  "meanSquaredDistance": number,
  "clusters": [
    {
      object (Cluster)
    }
  ]
}
```

| Fields                |                                                                                                                                                                 |
|-----------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `daviesBouldinIndex`  | `number` Davies-Bouldin index.                                                                                                                                  |
| `meanSquaredDistance` | `number` Mean of squared distances between each sample to its cluster centroid.                                                                                 |
| `clusters[]`          | `object ( `[`Cluster`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.Cluster)` )` Information for all clusters. |

### Cluster

**JSON representation**

```
{
  "centroidId": string,
  "featureValues": [
    {
      object (FeatureValue)
    }
  ],
  "count": string
}
```

| Fields            |                                                                                                                                                                                                 |
|-------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `centroidId`      | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Centroid id.                                                                                             |
| `featureValues[]` | `object ( `[`FeatureValue`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.FeatureValue)` )` Values of highly variant features for this cluster. |
| `count`           | `string ( `[`Int64Value`](https://developers.google.com/discovery/v1/type-format)` format)` Count of training data rows that were assigned to this cluster.                                     |

### FeatureValue

**JSON representation**

```
{
  "featureColumn": string,

  // Union field value can be only one of the following:
  "numericalValue": number,
  "categoricalValue": {
    object (CategoricalValue)
  }
  // End of list of possible types for union field value.
}
```

| Fields                                                                 |                                                                                                                                                                                    |
|------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `featureColumn`                                                        | `string` The feature column name.                                                                                                                                                  |
| Union field `value` . Value. `value` can be only one of the following: |                                                                                                                                                                                    |
| `numericalValue`                                                       | `number` The numerical feature value. This is the centroid value for this feature.                                                                                                 |
| `categoricalValue`                                                     | `object ( `[`CategoricalValue`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.CategoricalValue)` )` The categorical feature value. |
|                                                                        |                                                                                                                                                                                    |

### CategoricalValue

**JSON representation**

```
{
  "categoryCounts": [
    {
      object (CategoryCount)
    }
  ]
}
```

| Fields             |                                                                                                                                                                                                                                                                                                                                                                                            |
|--------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `categoryCounts[]` | `object ( `[`CategoryCount`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.CategoryCount)` )` Counts of all categories for the categorical feature. If there are more than ten categories, we return top ten (by count) and return one more CategoryCount with category "\_OTHER\_" and count as aggregate counts of remaining categories. |

### CategoryCount

**JSON representation**

```
{
  "category": string,
  "count": string
}
```

| Fields     |                                                                                                                                                                     |
|------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `category` | `string` The name of category.                                                                                                                                      |
| `count`    | `string ( `[`Int64Value`](https://developers.google.com/discovery/v1/type-format)` format)` The count of training samples matching the category within the cluster. |

### RankingMetrics

**JSON representation**

```
{
  "meanAveragePrecision": number,
  "meanSquaredError": number,
  "normalizedDiscountedCumulativeGain": number,
  "averageRank": number
}
```

| Fields                               |                                                                                                                                                                                                                                                                           |
|--------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `meanAveragePrecision`               | `number` Calculates a precision per user for all the items by ranking them and then averages all the precisions across all the users.                                                                                                                                     |
| `meanSquaredError`                   | `number` Similar to the mean squared error computed in regression and explicit recommendation models except instead of computing the rating directly, the output from evaluate is computed against a preference which is 1 or 0 depending on if the rating exists or not. |
| `normalizedDiscountedCumulativeGain` | `number` A metric to determine the goodness of a ranking calculated from the predicted confidence by comparing it to an ideal rank measured by the original ratings.                                                                                                      |
| `averageRank`                        | `number` Determines the goodness of a ranking by computing the percentile rank from the predicted confidence and dividing it by the original rank.                                                                                                                        |

### ArimaForecastingMetrics

**JSON representation**

```
{
  "nonSeasonalOrder": [
    {
      object (ArimaOrder)
    }
  ],
  "arimaFittingMetrics": [
    {
      object (ArimaFittingMetrics)
    }
  ],
  "seasonalPeriods": [
    enum (SeasonalPeriodType)
  ],
  "hasDrift": [
    boolean
  ],
  "timeSeriesId": [
    string
  ],
  "arimaSingleModelForecastingMetrics": [
    {
      object (ArimaSingleModelForecastingMetrics)
    }
  ]
}
```

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
<td><code>nonSeasonalOrder[] </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.ArimaOrder"><code>ArimaOrder</code></a><code> )</code></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>Non-seasonal order.</p></td>
</tr>
<tr class="even">
<td><code>arimaFittingMetrics[] </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.ArimaFittingMetrics"><code>ArimaFittingMetrics</code></a><code> )</code></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>Arima model fitting metrics.</p></td>
</tr>
<tr class="odd">
<td><code>seasonalPeriods[] </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>enum ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.SeasonalPeriodType"><code>SeasonalPeriodType</code></a><code> )</code></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>Seasonal periods. Repeated because multiple periods are supported for one time series.</p></td>
</tr>
<tr class="even">
<td><code>hasDrift[] </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>boolean</code></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>Whether Arima model fitted with drift or not. It is always false when d is not 1.</p></td>
</tr>
<tr class="odd">
<td><code>timeSeriesId[] </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>string</code></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>Id to differentiate different time series for the large-scale case.</p></td>
</tr>
<tr class="even">
<td><code>arimaSingleModelForecastingMetrics[]</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.ArimaSingleModelForecastingMetrics"><code>ArimaSingleModelForecastingMetrics</code></a><code> )</code></p>
<p>Repeated as there can be many metric sets (one for each model) in auto-arima and the large-scale case.</p></td>
</tr>
</tbody>
</table>

### ArimaSingleModelForecastingMetrics

**JSON representation**

```
{
  "nonSeasonalOrder": {
    object (ArimaOrder)
  },
  "arimaFittingMetrics": {
    object (ArimaFittingMetrics)
  },
  "hasDrift": boolean,
  "timeSeriesId": string,
  "timeSeriesIds": [
    string
  ],
  "seasonalPeriods": [
    enum (SeasonalPeriodType)
  ],
  "hasHolidayEffect": boolean,
  "hasSpikesAndDips": boolean,
  "hasStepChanges": boolean
}
```

| Fields                |                                                                                                                                                                                                                                                                                                                                                |
|-----------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `nonSeasonalOrder`    | `object ( `[`ArimaOrder`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.ArimaOrder)` )` Non-seasonal order.                                                                                                                                                                                    |
| `arimaFittingMetrics` | `object ( `[`ArimaFittingMetrics`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.ArimaFittingMetrics)` )` Arima fitting metrics.                                                                                                                                                               |
| `hasDrift`            | `boolean` Is arima model fitted with drift or not. It is always false when d is not 1.                                                                                                                                                                                                                                                         |
| `timeSeriesId`        | `string` The time_series_id value for this time series. It will be one of the unique values from the time_series_id_column specified during ARIMA model training. Only present when time_series_id_column training option was used.                                                                                                            |
| `timeSeriesIds[]`     | `string` The tuple of time_series_ids identifying this time series. It will be one of the unique tuples of values present in the time_series_id_columns specified during ARIMA model training. Only present when time_series_id_columns training option was used and the order of values here are same as the order of time_series_id_columns. |
| `seasonalPeriods[]`   | `enum ( `[`SeasonalPeriodType`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.SeasonalPeriodType)` )` Seasonal periods. Repeated because multiple periods are supported for one time series.                                                                                                   |
| `hasHolidayEffect`    | `boolean` If true, holiday_effect is a part of time series decomposition result.                                                                                                                                                                                                                                                               |
| `hasSpikesAndDips`    | `boolean` If true, spikes_and_dips is a part of time series decomposition result.                                                                                                                                                                                                                                                              |
| `hasStepChanges`      | `boolean` If true, step_changes is a part of time series decomposition result.                                                                                                                                                                                                                                                                 |

### DimensionalityReductionMetrics

**JSON representation**

```
{
  "totalExplainedVarianceRatio": number
}
```

| Fields                        |                                                                                       |
|-------------------------------|---------------------------------------------------------------------------------------|
| `totalExplainedVarianceRatio` | `number` Total percentage of variance explained by the selected principal components. |

### ExportDataStatistics

**JSON representation**

```
{
  "fileCount": string,
  "rowCount": string
}
```

| Fields      |                                                                                                                                                                                   |
|-------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `fileCount` | `string ( `[`Int64Value`](https://developers.google.com/discovery/v1/type-format)` format)` Number of destination files generated in case of EXPORT DATA statement only.          |
| `rowCount`  | `string ( `[`Int64Value`](https://developers.google.com/discovery/v1/type-format)` format)` \[Alpha\] Number of destination rows generated in case of EXPORT DATA statement only. |

### ExternalServiceCost

**JSON representation**

```
{
  "externalService": string,
  "bytesProcessed": string,
  "bytesBilled": string,
  "slotMs": string,
  "reservedSlotCount": string,
  "billingMethod": string
}
```

| Fields              |                                                                                                                                                                                                                                                                                 |
|---------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `externalService`   | `string` External service name.                                                                                                                                                                                                                                                 |
| `bytesProcessed`    | `string ( `[`Int64Value`](https://developers.google.com/discovery/v1/type-format)` format)` External service cost in terms of bigquery bytes processed.                                                                                                                         |
| `bytesBilled`       | `string ( `[`Int64Value`](https://developers.google.com/discovery/v1/type-format)` format)` External service cost in terms of bigquery bytes billed.                                                                                                                            |
| `slotMs`            | `string ( `[`Int64Value`](https://developers.google.com/discovery/v1/type-format)` format)` External service cost in terms of bigquery slot milliseconds.                                                                                                                       |
| `reservedSlotCount` | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Non-preemptable reserved slots used for external job. For example, reserved slots for Cloua AI Platform job are the VM usages converted to BigQuery slot with equivalent mount of price. |
| `billingMethod`     | `string` The billing method used for the external job. This field, set to `SERVICES_SKU` , is only used when billing under the services SKU. Otherwise, it is unspecified for backward compatibility.                                                                           |

### BiEngineStatistics

**JSON representation**

```
{
  "biEngineMode": enum (BiEngineMode),
  "accelerationMode": enum (BiEngineAccelerationMode),
  "biEngineReasons": [
    {
      object (BiEngineReason)
    }
  ]
}
```

| Fields              |                                                                                                                                                                                                                                                                                                                                                     |
|---------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `biEngineMode`      | `enum ( `[`BiEngineMode`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.BiEngineMode)` )` Output only. Specifies which mode of BI Engine acceleration was performed (if any).                                                                                                                       |
| `accelerationMode`  | `enum ( `[`BiEngineAccelerationMode`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.BiEngineAccelerationMode)` )` Output only. Specifies which mode of BI Engine acceleration was performed (if any).                                                                                               |
| `biEngineReasons[]` | `object ( `[`BiEngineReason`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.BiEngineReason)` )` In case of DISABLED or PARTIAL bi_engine_mode, these contain the explanatory reasons as to why BI Engine could not accelerate. In case the full query was accelerated, this field is not populated. |

### BiEngineReason

**JSON representation**

```
{
  "code": enum (Code),
  "message": string
}
```

| Fields    |                                                                                                                                                                                                         |
|-----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `code`    | `enum ( `[`Code`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.Code)` )` Output only. High-level BI Engine reason for partial or disabled acceleration |
| `message` | `string` Output only. Free form human-readable reason for partial or disabled acceleration.                                                                                                             |

### LoadQueryStatistics

**JSON representation**

```
{
  "inputFiles": string,
  "inputFileBytes": string,
  "outputRows": string,
  "outputBytes": string,
  "badRecords": string,
  "bytesTransferred": string
}
```

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
<td><code>inputFiles</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>Int64Value</code></a><code> format)</code></p>
<p>Output only. Number of source files in a LOAD query.</p></td>
</tr>
<tr class="even">
<td><code>inputFileBytes</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>Int64Value</code></a><code> format)</code></p>
<p>Output only. Number of bytes of source data in a LOAD query.</p></td>
</tr>
<tr class="odd">
<td><code>outputRows</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>Int64Value</code></a><code> format)</code></p>
<p>Output only. Number of rows imported in a LOAD query. Note that while a LOAD query is in the running state, this value may change.</p></td>
</tr>
<tr class="even">
<td><code>outputBytes</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>Int64Value</code></a><code> format)</code></p>
<p>Output only. Size of the loaded data in bytes. Note that while a LOAD query is in the running state, this value may change.</p></td>
</tr>
<tr class="odd">
<td><code>badRecords</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>Int64Value</code></a><code> format)</code></p>
<p>Output only. The number of bad records encountered while processing a LOAD query. Note that if the job has failed because of more bad records encountered than the maximum allowed in the load job configuration, then this number can be less than the total number of bad records present in the input data.</p></td>
</tr>
<tr class="even">
<td><code>bytesTransferred </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>Int64Value</code></a><code> format)</code></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>Output only. This field is deprecated. The number of bytes of source data copied over the network for a <code>LOAD</code> query. <code>transferred_bytes</code> has the canonical value for physical transferred bytes, which is used for BigQuery Omni billing.</p></td>
</tr>
</tbody>
</table>

### SearchStatistics

**JSON representation**

```
{
  "indexUsageMode": enum (IndexUsageMode),
  "indexUnusedReasons": [
    {
      object (IndexUnusedReason)
    }
  ],
  "indexPruningStats": [
    {
      object (IndexPruningStats)
    }
  ]
}
```

| Fields                 |                                                                                                                                                                                                                                                                                                                                                                                                     |
|------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `indexUsageMode`       | `enum ( `[`IndexUsageMode`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.IndexUsageMode)` )` Specifies the index usage mode for the query.                                                                                                                                                                                                         |
| `indexUnusedReasons[]` | `object ( `[`IndexUnusedReason`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.IndexUnusedReason)` )` When `indexUsageMode` is `UNUSED` or `PARTIALLY_USED` , this field explains why indexes were not used in all or part of the search query. If `indexUsageMode` is `FULLY_USED` , this field is not populated.                                  |
| `indexPruningStats[]`  | `object ( `[`IndexPruningStats`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.IndexPruningStats)` )` Search index pruning statistics, one for each base table that has a search index. If a base table does not have a search index or the index does not help with pruning on the base table, then there is no pruning statistics for that table. |

### IndexUnusedReason

**JSON representation**

```
{

  // Union field _code can be only one of the following:
  "code": enum (Code)
  // End of list of possible types for union field _code.

  // Union field _message can be only one of the following:
  "message": string
  // End of list of possible types for union field _message.

  // Union field _base_table can be only one of the following:
  "baseTable": {
    object (TableReference)
  }
  // End of list of possible types for union field _base_table.

  // Union field _index_name can be only one of the following:
  "indexName": string
  // End of list of possible types for union field _index_name.
}
```

| Fields                                                                      |                                                                                                                                                                                                                                      |
|-----------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `_code` . `_code` can be only one of the following:             |                                                                                                                                                                                                                                      |
| `code`                                                                      | `enum ( `[`Code`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.Code_1)` )` Specifies the high-level reason for the scenario when no search index was used.                          |
|                                                                             |                                                                                                                                                                                                                                      |
| Union field `_message` . `_message` can be only one of the following:       |                                                                                                                                                                                                                                      |
| `message`                                                                   | `string` Free form human-readable reason for the scenario when no search index was used.                                                                                                                                             |
|                                                                             |                                                                                                                                                                                                                                      |
| Union field `_base_table` . `_base_table` can be only one of the following: |                                                                                                                                                                                                                                      |
| `baseTable`                                                                 | `object ( `[`TableReference`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_dataset_info#Output.Schema.TableReference)` )` Specifies the base table involved in the reason that no search index was used. |
|                                                                             |                                                                                                                                                                                                                                      |
| Union field `_index_name` . `_index_name` can be only one of the following: |                                                                                                                                                                                                                                      |
| `indexName`                                                                 | `string` Specifies the name of the unused search index, if available.                                                                                                                                                                |
|                                                                             |                                                                                                                                                                                                                                      |

### IndexPruningStats

**JSON representation**

```
{

  // Union field _base_table can be only one of the following:
  "baseTable": {
    object (TableReference)
  }
  // End of list of possible types for union field _base_table.

  // Union field _index_id can be only one of the following:
  "indexId": string
  // End of list of possible types for union field _index_id.

  // Union field _pre_index_pruning_parallel_input_count can be only one of the
  // following:
  "preIndexPruningParallelInputCount": string
  // End of list of possible types for union field
  // _pre_index_pruning_parallel_input_count.

  // Union field _post_index_pruning_parallel_input_count can be only one of the
  // following:
  "postIndexPruningParallelInputCount": string
  // End of list of possible types for union field
  // _post_index_pruning_parallel_input_count.
}
```

| Fields                                                                                                                                |                                                                                                                                                                                 |
|---------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `_base_table` . `_base_table` can be only one of the following:                                                           |                                                                                                                                                                                 |
| `baseTable`                                                                                                                           | `object ( `[`TableReference`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_dataset_info#Output.Schema.TableReference)` )` The base table reference. |
|                                                                                                                                       |                                                                                                                                                                                 |
| Union field `_index_id` . `_index_id` can be only one of the following:                                                               |                                                                                                                                                                                 |
| `indexId`                                                                                                                             | `string` The index id.                                                                                                                                                          |
|                                                                                                                                       |                                                                                                                                                                                 |
| Union field `_pre_index_pruning_parallel_input_count` . `_pre_index_pruning_parallel_input_count` can be only one of the following:   |                                                                                                                                                                                 |
| `preIndexPruningParallelInputCount`                                                                                                   | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` The number of parallel inputs before index pruning.                                      |
|                                                                                                                                       |                                                                                                                                                                                 |
| Union field `_post_index_pruning_parallel_input_count` . `_post_index_pruning_parallel_input_count` can be only one of the following: |                                                                                                                                                                                 |
| `postIndexPruningParallelInputCount`                                                                                                  | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` The number of parallel inputs after index pruning.                                       |
|                                                                                                                                       |                                                                                                                                                                                 |

### VectorSearchStatistics

**JSON representation**

```
{
  "indexUsageMode": enum (IndexUsageMode),
  "indexUnusedReasons": [
    {
      object (IndexUnusedReason)
    }
  ],
  "storedColumnsUsages": [
    {
      object (StoredColumnsUsage)
    }
  ]
}
```

| Fields                  |                                                                                                                                                                                                                                                                                                                                                                           |
|-------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `indexUsageMode`        | `enum ( `[`IndexUsageMode`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.IndexUsageMode_1)` )` Specifies the index usage mode for the query.                                                                                                                                                                             |
| `indexUnusedReasons[]`  | `object ( `[`IndexUnusedReason`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.IndexUnusedReason)` )` When `indexUsageMode` is `UNUSED` or `PARTIALLY_USED` , this field explains why indexes were not used in all or part of the vector search query. If `indexUsageMode` is `FULLY_USED` , this field is not populated. |
| `storedColumnsUsages[]` | `object ( `[`StoredColumnsUsage`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.StoredColumnsUsage)` )` Specifies the usage of stored columns in the query when stored columns are used in the query.                                                                                                                     |

### StoredColumnsUsage

**JSON representation**

```
{
  "storedColumnsUnusedReasons": [
    {
      object (StoredColumnsUnusedReason)
    }
  ],

  // Union field _is_query_accelerated can be only one of the following:
  "isQueryAccelerated": boolean
  // End of list of possible types for union field _is_query_accelerated.

  // Union field _base_table can be only one of the following:
  "baseTable": {
    object (TableReference)
  }
  // End of list of possible types for union field _base_table.
}
```

| Fields                                                                                          |                                                                                                                                                                                                                     |
|-------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `storedColumnsUnusedReasons[]`                                                                  | `object ( `[`StoredColumnsUnusedReason`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.StoredColumnsUnusedReason)` )` If stored columns were not used, explain why. |
| Union field `_is_query_accelerated` . `_is_query_accelerated` can be only one of the following: |                                                                                                                                                                                                                     |
| `isQueryAccelerated`                                                                            | `boolean` Specifies whether the query was accelerated with stored columns.                                                                                                                                          |
|                                                                                                 |                                                                                                                                                                                                                     |
| Union field `_base_table` . `_base_table` can be only one of the following:                     |                                                                                                                                                                                                                     |
| `baseTable`                                                                                     | `object ( `[`TableReference`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_dataset_info#Output.Schema.TableReference)` )` Specifies the base table.                                     |
|                                                                                                 |                                                                                                                                                                                                                     |

### StoredColumnsUnusedReason

**JSON representation**

```
{
  "uncoveredColumns": [
    string
  ],

  // Union field _code can be only one of the following:
  "code": enum (Code)
  // End of list of possible types for union field _code.

  // Union field _message can be only one of the following:
  "message": string
  // End of list of possible types for union field _message.
}
```

| Fields                                                                |                                                                                                                                                                                                                               |
|-----------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `uncoveredColumns[]`                                                  | `string` Specifies which columns were not covered by the stored columns for the specified code up to 20 columns. This is populated when the code is STORED_COLUMNS_COVER_INSUFFICIENT and BASE_TABLE_HAS_CLS.                 |
| Union field `_code` . `_code` can be only one of the following:       |                                                                                                                                                                                                                               |
| `code`                                                                | `enum ( `[`Code`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.Code_2)` )` Specifies the high-level reason for the unused scenario, each reason must have a code associated. |
|                                                                       |                                                                                                                                                                                                                               |
| Union field `_message` . `_message` can be only one of the following: |                                                                                                                                                                                                                               |
| `message`                                                             | `string` Specifies the detailed description for the scenario.                                                                                                                                                                 |
|                                                                       |                                                                                                                                                                                                                               |

### PerformanceInsights

**JSON representation**

```
{
  "avgPreviousExecutionMs": string,
  "stagePerformanceStandaloneInsights": [
    {
      object (StagePerformanceStandaloneInsight)
    }
  ],
  "stagePerformanceChangeInsights": [
    {
      object (StagePerformanceChangeInsight)
    }
  ],
  "tableChangeInsights": [
    {
      object (TableChangeInsight)
    }
  ]
}
```

| Fields                                 |                                                                                                                                                                                                                                                                                                         |
|----------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `avgPreviousExecutionMs`               | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Output only. Average execution ms of previous runs. Indicates the job ran slow compared to previous executions. To find previous executions, use INFORMATION_SCHEMA tables and filter jobs with same query hash. |
| `stagePerformanceStandaloneInsights[]` | `object ( `[`StagePerformanceStandaloneInsight`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.StagePerformanceStandaloneInsight)` )` Output only. Standalone query stage performance insights, for exploring potential improvements.                   |
| `stagePerformanceChangeInsights[]`     | `object ( `[`StagePerformanceChangeInsight`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.StagePerformanceChangeInsight)` )` Output only. Query stage performance insights compared to previous runs, for diagnosing performance regression.           |
| `tableChangeInsights[]`                | `object ( `[`TableChangeInsight`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.TableChangeInsight)` )` Output only. Performance insights for table-level attributes that changed compared to previous runs.                                            |

### StagePerformanceStandaloneInsight

**JSON representation**

```
{
  "stageId": string,
  "biEngineReasons": [
    {
      object (BiEngineReason)
    }
  ],
  "highCardinalityJoins": [
    {
      object (HighCardinalityJoin)
    }
  ],

  // Union field _slot_contention can be only one of the following:
  "slotContention": boolean
  // End of list of possible types for union field _slot_contention.

  // Union field _insufficient_shuffle_quota can be only one of the following:
  "insufficientShuffleQuota": boolean
  // End of list of possible types for union field _insufficient_shuffle_quota.

  // Union field _partition_skew can be only one of the following:
  "partitionSkew": {
    object (PartitionSkew)
  }
  // End of list of possible types for union field _partition_skew.
}
```

| Fields                                                                                                      |                                                                                                                                                                                                                                                               |
|-------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `stageId`                                                                                                   | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Output only. The stage id that the insight mapped to.                                                                                                                  |
| `biEngineReasons[]`                                                                                         | `object ( `[`BiEngineReason`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.BiEngineReason)` )` Output only. If present, the stage had the following reasons for being disqualified from BI Engine execution. |
| `highCardinalityJoins[]`                                                                                    | `object ( `[`HighCardinalityJoin`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.HighCardinalityJoin)` )` Output only. High cardinality joins in the stage.                                                   |
| Union field `_slot_contention` . `_slot_contention` can be only one of the following:                       |                                                                                                                                                                                                                                                               |
| `slotContention`                                                                                            | `boolean` Output only. True if the stage has a slot contention issue.                                                                                                                                                                                         |
|                                                                                                             |                                                                                                                                                                                                                                                               |
| Union field `_insufficient_shuffle_quota` . `_insufficient_shuffle_quota` can be only one of the following: |                                                                                                                                                                                                                                                               |
| `insufficientShuffleQuota`                                                                                  | `boolean` Output only. True if the stage has insufficient shuffle quota.                                                                                                                                                                                      |
|                                                                                                             |                                                                                                                                                                                                                                                               |
| Union field `_partition_skew` . `_partition_skew` can be only one of the following:                         |                                                                                                                                                                                                                                                               |
| `partitionSkew`                                                                                             | `object ( `[`PartitionSkew`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.PartitionSkew)` )` Output only. Partition skew in the stage.                                                                       |
|                                                                                                             |                                                                                                                                                                                                                                                               |

### HighCardinalityJoin

**JSON representation**

```
{
  "leftRows": string,
  "rightRows": string,
  "outputRows": string,
  "stepIndex": integer
}
```

| Fields       |                                                                                                                                |
|--------------|--------------------------------------------------------------------------------------------------------------------------------|
| `leftRows`   | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Output only. Count of left input rows.  |
| `rightRows`  | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Output only. Count of right input rows. |
| `outputRows` | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Output only. Count of the output rows.  |
| `stepIndex`  | `integer` Output only. The index of the join operator in the ExplainQueryStep lists.                                           |

### PartitionSkew

**JSON representation**

```
{
  "skewSources": [
    {
      object (SkewSource)
    }
  ]
}
```

| Fields          |                                                                                                                                                                                               |
|-----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `skewSources[]` | `object ( `[`SkewSource`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.SkewSource)` )` Output only. Source stages which produce skewed data. |

### SkewSource

**JSON representation**

```
{
  "stageId": string,
  "outputBytesMedian": string,
  "outputBytesP95": string,
  "outputBytesMax": string
}
```

| Fields              |                                                                                                                                                                          |
|---------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `stageId`           | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Output only. Stage id of the skew source stage.                                   |
| `outputBytesMedian` | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Output only. Median partition output size (in bytes) for this stage.              |
| `outputBytesP95`    | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Output only. 95-th percentile of partition output size (in bytes) for this stage. |
| `outputBytesMax`    | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Output only. Max partition output size (in bytes) for this stage.                 |

### StagePerformanceChangeInsight

**JSON representation**

```
{
  "stageId": string,

  // Union field _input_data_change can be only one of the following:
  "inputDataChange": {
    object (InputDataChange)
  }
  // End of list of possible types for union field _input_data_change.
}
```

| Fields                                                                                    |                                                                                                                                                                                                              |
|-------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `stageId`                                                                                 | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Output only. The stage id that the insight mapped to.                                                                 |
| Union field `_input_data_change` . `_input_data_change` can be only one of the following: |                                                                                                                                                                                                              |
| `inputDataChange`                                                                         | `object ( `[`InputDataChange`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.InputDataChange)` )` Output only. Input data change insight of the query stage. |
|                                                                                           |                                                                                                                                                                                                              |

### InputDataChange

**JSON representation**

```
{
  "recordsReadDiffPercentage": number
}
```

| Fields                      |                                                                                      |
|-----------------------------|--------------------------------------------------------------------------------------|
| `recordsReadDiffPercentage` | `number` Output only. Records read difference percentage compared to a previous run. |

### TableChangeInsight

**JSON representation**

```
{
  "tableReference": {
    object (TableReference)
  },

  // Union field _metadata_cache_staleness_insight can be only one of the
  // following:
  "metadataCacheStalenessInsight": {
    object (MetadataCacheStalenessInsight)
  }
  // End of list of possible types for union field
  // _metadata_cache_staleness_insight.

  // Union field _metadata_cache_not_used_but_used_previously can be only one of
  // the following:
  "metadataCacheNotUsedButUsedPreviously": boolean
  // End of list of possible types for union field
  // _metadata_cache_not_used_but_used_previously.
}
```

| Fields                                                                                                                                        |                                                                                                                                                                                                                                                                                                                                                   |
|-----------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `tableReference`                                                                                                                              | `object ( `[`TableReference`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_dataset_info#Output.Schema.TableReference)` )` Output only. The table that was queried.                                                                                                                                                    |
| Union field `_metadata_cache_staleness_insight` . `_metadata_cache_staleness_insight` can be only one of the following:                       |                                                                                                                                                                                                                                                                                                                                                   |
| `metadataCacheStalenessInsight`                                                                                                               | `object ( `[`MetadataCacheStalenessInsight`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.MetadataCacheStalenessInsight)` )` Output only. If present, indicates that the table's metadata column index staleness has increased significantly compared to previous jobs with the same query hash. |
|                                                                                                                                               |                                                                                                                                                                                                                                                                                                                                                   |
| Union field `_metadata_cache_not_used_but_used_previously` . `_metadata_cache_not_used_but_used_previously` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                   |
| `metadataCacheNotUsedButUsedPreviously`                                                                                                       | `boolean` Output only. True if the table's column metadata index was not used in the current job, but was used in a previous job with the same query hash.                                                                                                                                                                                        |
|                                                                                                                                               |                                                                                                                                                                                                                                                                                                                                                   |

### MetadataCacheStalenessInsight

**JSON representation**

```
{
  "avgPreviousStalenessMs": string,
  "stalenessPercentageIncrease": number
}
```

| Fields                        |                                                                                                                                                                                                                                                                                                        |
|-------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `avgPreviousStalenessMs`      | `string ( `[`Duration`](https://protobuf.dev/reference/protobuf/google.protobuf/#duration)` format)` Output only. Average column metadata index staleness of previous runs with the same query hash. A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` . |
| `stalenessPercentageIncrease` | `number` Output only. The percent increase in staleness between the current job and the average staleness of previous jobs with the same query hash.                                                                                                                                                   |

### QueryInfo

**JSON representation**

```
{
  "optimizationDetails": {
    object
  }
}
```

| Fields                |                                                                                                                                                      |
|-----------------------|------------------------------------------------------------------------------------------------------------------------------------------------------|
| `optimizationDetails` | `object ( `[`Struct`](https://protobuf.dev/reference/protobuf/google.protobuf/#struct)` format)` Output only. Information about query optimizations. |

### SparkStatistics

**JSON representation**

```
{
  "endpoints": {
    string: string,
    ...
  },

  // Union field _spark_job_id can be only one of the following:
  "sparkJobId": string
  // End of list of possible types for union field _spark_job_id.

  // Union field _spark_job_location can be only one of the following:
  "sparkJobLocation": string
  // End of list of possible types for union field _spark_job_location.

  // Union field _logging_info can be only one of the following:
  "loggingInfo": {
    object (LoggingInfo)
  }
  // End of list of possible types for union field _logging_info.

  // Union field _kms_key_name can be only one of the following:
  "kmsKeyName": string
  // End of list of possible types for union field _kms_key_name.

  // Union field _gcs_staging_bucket can be only one of the following:
  "gcsStagingBucket": string
  // End of list of possible types for union field _gcs_staging_bucket.
}
```

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
<td><code>endpoints</code></td>
<td><p><code>map (key: string, value: string)</code></p>
<p>Output only. Endpoints returned from Dataproc. Key list: - history_server_endpoint: A link to Spark job UI.</p>
<p>An object containing a list of <code>"key": value</code> pairs. Example: <code>{ "name": "wrench", "mass": "1.3kg", "count": "3" }</code> .</p></td>
</tr>
<tr class="even">
<td><p>Union field <code>_spark_job_id</code> .</p>
<p><code>_spark_job_id</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="odd">
<td><code>sparkJobId</code></td>
<td><p><code>string</code></p>
<p>Output only. Spark job ID if a Spark job is created successfully.</p></td>
</tr>
<tr class="even">
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p>Union field <code>_spark_job_location</code> .</p>
<p><code>_spark_job_location</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="even">
<td><code>sparkJobLocation</code></td>
<td><p><code>string</code></p>
<p>Output only. Location where the Spark job is executed. A location is selected by BigQueury for jobs configured to run in a multi-region.</p></td>
</tr>
<tr class="odd">
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p>Union field <code>_logging_info</code> .</p>
<p><code>_logging_info</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="odd">
<td><code>loggingInfo</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.LoggingInfo"><code>LoggingInfo</code></a><code> )</code></p>
<p>Output only. Logging info is used to generate a link to Cloud Logging.</p></td>
</tr>
<tr class="even">
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p>Union field <code>_kms_key_name</code> .</p>
<p><code>_kms_key_name</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="even">
<td><code>kmsKeyName</code></td>
<td><p><code>string</code></p>
<p>Output only. The Cloud KMS encryption key that is used to protect the resources created by the Spark job. If the Spark procedure uses the invoker security mode, the Cloud KMS encryption key is either inferred from the provided system variable, <code>@@spark_proc_properties.kms_key_name</code> , or the default key of the BigQuery job's project (if the CMEK organization policy is enforced). Otherwise, the Cloud KMS key is either inferred from the Spark connection associated with the procedure (if it is provided), or from the default key of the Spark connection's project if the CMEK organization policy is enforced.</p>
<p>Example:</p>
<ul>
<li><code>projects/[kms_project_id]/locations/[region]/keyRings/[key_region]/cryptoKeys/[key]</code></li>
</ul></td>
</tr>
<tr class="odd">
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p>Union field <code>_gcs_staging_bucket</code> .</p>
<p><code>_gcs_staging_bucket</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="odd">
<td><code>gcsStagingBucket</code></td>
<td><p><code>string</code></p>
<p>Output only. The Google Cloud Storage bucket that is used as the default file system by the Spark application. This field is only filled when the Spark procedure uses the invoker security mode. The <code>gcsStagingBucket</code> bucket is inferred from the <code>@@spark_proc_properties.staging_bucket</code> system variable (if it is provided). Otherwise, BigQuery creates a default staging bucket for the job and returns the bucket name in this field.</p>
<p>Example:</p>
<ul>
<li><code>gs://[bucket_name]</code></li>
</ul></td>
</tr>
<tr class="even">
<td></td>
<td></td>
</tr>
</tbody>
</table>

### EndpointsEntry

**JSON representation**

```
{
  "key": string,
  "value": string
}
```

| Fields  |          |
|---------|----------|
| `key`   | `string` |
| `value` | `string` |

### LoggingInfo

**JSON representation**

```
{
  "resourceType": string,
  "projectId": string
}
```

| Fields         |                                                                     |
|----------------|---------------------------------------------------------------------|
| `resourceType` | `string` Output only. Resource type used for logging.               |
| `projectId`    | `string` Output only. Project ID where the Spark logs were written. |

### MaterializedViewStatistics

**JSON representation**

```
{
  "materializedView": [
    {
      object (MaterializedView)
    }
  ]
}
```

| Fields               |                                                                                                                                                                                                                                                                                                                                                                          |
|----------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `materializedView[]` | `object ( `[`MaterializedView`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.MaterializedView)` )` Materialized views considered for the query job. Only certain materialized views are used. For a detailed list, see the child message. If many materialized views are considered, then the list might be incomplete. |

### MaterializedView

**JSON representation**

```
{

  // Union field _table_reference can be only one of the following:
  "tableReference": {
    object (TableReference)
  }
  // End of list of possible types for union field _table_reference.

  // Union field _chosen can be only one of the following:
  "chosen": boolean
  // End of list of possible types for union field _chosen.

  // Union field _estimated_bytes_saved can be only one of the following:
  "estimatedBytesSaved": string
  // End of list of possible types for union field _estimated_bytes_saved.

  // Union field _rejected_reason can be only one of the following:
  "rejectedReason": enum (RejectedReason)
  // End of list of possible types for union field _rejected_reason.
}
```

| Fields                                                                                            |                                                                                                                                                                                                                                                                                                                   |
|---------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `_table_reference` . `_table_reference` can be only one of the following:             |                                                                                                                                                                                                                                                                                                                   |
| `tableReference`                                                                                  | `object ( `[`TableReference`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_dataset_info#Output.Schema.TableReference)` )` The candidate materialized view.                                                                                                                            |
|                                                                                                   |                                                                                                                                                                                                                                                                                                                   |
| Union field `_chosen` . `_chosen` can be only one of the following:                               |                                                                                                                                                                                                                                                                                                                   |
| `chosen`                                                                                          | `boolean` Whether the materialized view is chosen for the query. A materialized view can be chosen to rewrite multiple parts of the same query. If a materialized view is chosen to rewrite any part of the query, then this field is true, even if the materialized view was not chosen to rewrite others parts. |
|                                                                                                   |                                                                                                                                                                                                                                                                                                                   |
| Union field `_estimated_bytes_saved` . `_estimated_bytes_saved` can be only one of the following: |                                                                                                                                                                                                                                                                                                                   |
| `estimatedBytesSaved`                                                                             | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` If present, specifies a best-effort estimation of the bytes saved by using the materialized view rather than its base tables.                                                                                              |
|                                                                                                   |                                                                                                                                                                                                                                                                                                                   |
| Union field `_rejected_reason` . `_rejected_reason` can be only one of the following:             |                                                                                                                                                                                                                                                                                                                   |
| `rejectedReason`                                                                                  | `enum ( `[`RejectedReason`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.RejectedReason)` )` If present, specifies the reason why the materialized view was not chosen for the query.                                                                            |
|                                                                                                   |                                                                                                                                                                                                                                                                                                                   |

### MetadataCacheStatistics

**JSON representation**

```
{
  "tableMetadataCacheUsage": [
    {
      object (TableMetadataCacheUsage)
    }
  ]
}
```

| Fields                      |                                                                                                                                                                                                                                         |
|-----------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `tableMetadataCacheUsage[]` | `object ( `[`TableMetadataCacheUsage`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.TableMetadataCacheUsage)` )` Set for the Metadata caching eligible tables referenced in the query. |

### TableMetadataCacheUsage

**JSON representation**

```
{
  "staleness": string,
  "tableType": string,

  // Union field _table_reference can be only one of the following:
  "tableReference": {
    object (TableReference)
  }
  // End of list of possible types for union field _table_reference.

  // Union field _unused_reason can be only one of the following:
  "unusedReason": enum (UnusedReason)
  // End of list of possible types for union field _unused_reason.

  // Union field _explanation can be only one of the following:
  "explanation": string
  // End of list of possible types for union field _explanation.

  // Union field _pruning_stats can be only one of the following:
  "pruningStats": {
    object (PruningStats)
  }
  // End of list of possible types for union field _pruning_stats.
}
```

| Fields                                                                                |                                                                                                                                                                                                                                                                                                                                |
|---------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `staleness`                                                                           | `string ( `[`Duration`](https://protobuf.dev/reference/protobuf/google.protobuf/#duration)` format)` Duration since last refresh as of this job for managed tables (indicates metadata cache staleness as seen by this job). A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` . |
| `tableType`                                                                           | `string` [Table type](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#Table.FIELDS.type) .                                                                                                                                                                                                                     |
| Union field `_table_reference` . `_table_reference` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                |
| `tableReference`                                                                      | `object ( `[`TableReference`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_dataset_info#Output.Schema.TableReference)` )` Metadata caching eligible table referenced in the query.                                                                                                                 |
|                                                                                       |                                                                                                                                                                                                                                                                                                                                |
| Union field `_unused_reason` . `_unused_reason` can be only one of the following:     |                                                                                                                                                                                                                                                                                                                                |
| `unusedReason`                                                                        | `enum ( `[`UnusedReason`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.UnusedReason)` )` Reason for not using metadata caching for the table.                                                                                                                                 |
|                                                                                       |                                                                                                                                                                                                                                                                                                                                |
| Union field `_explanation` . `_explanation` can be only one of the following:         |                                                                                                                                                                                                                                                                                                                                |
| `explanation`                                                                         | `string` Free form human-readable reason metadata caching was unused for the job.                                                                                                                                                                                                                                              |
|                                                                                       |                                                                                                                                                                                                                                                                                                                                |
| Union field `_pruning_stats` . `_pruning_stats` can be only one of the following:     |                                                                                                                                                                                                                                                                                                                                |
| `pruningStats`                                                                        | `object ( `[`PruningStats`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.PruningStats)` )` The column metadata index pruning statistics.                                                                                                                                      |
|                                                                                       |                                                                                                                                                                                                                                                                                                                                |

### PruningStats

**JSON representation**

```
{

  // Union field _post_cmeta_pruning_partition_count can be only one of the
  // following:
  "postCmetaPruningPartitionCount": string
  // End of list of possible types for union field
  // _post_cmeta_pruning_partition_count.

  // Union field _pre_cmeta_pruning_parallel_input_count can be only one of the
  // following:
  "preCmetaPruningParallelInputCount": string
  // End of list of possible types for union field
  // _pre_cmeta_pruning_parallel_input_count.

  // Union field _post_cmeta_pruning_parallel_input_count can be only one of the
  // following:
  "postCmetaPruningParallelInputCount": string
  // End of list of possible types for union field
  // _post_cmeta_pruning_parallel_input_count.
}
```

| Fields                                                                                                                                |                                                                                                                               |
|---------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------|
| Union field `_post_cmeta_pruning_partition_count` . `_post_cmeta_pruning_partition_count` can be only one of the following:           |                                                                                                                               |
| `postCmetaPruningPartitionCount`                                                                                                      | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` The number of partitions matched.      |
|                                                                                                                                       |                                                                                                                               |
| Union field `_pre_cmeta_pruning_parallel_input_count` . `_pre_cmeta_pruning_parallel_input_count` can be only one of the following:   |                                                                                                                               |
| `preCmetaPruningParallelInputCount`                                                                                                   | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` The number of parallel inputs scanned. |
|                                                                                                                                       |                                                                                                                               |
| Union field `_post_cmeta_pruning_parallel_input_count` . `_post_cmeta_pruning_parallel_input_count` can be only one of the following: |                                                                                                                               |
| `postCmetaPruningParallelInputCount`                                                                                                  | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` The number of parallel inputs matched. |
|                                                                                                                                       |                                                                                                                               |

### IncrementalResultStats

**JSON representation**

```
{
  "disabledReason": enum (DisabledReason),
  "disabledReasonDetails": string,
  "resultSetLastReplaceTime": string,
  "resultSetLastModifyTime": string,
  "firstIncrementalRowTime": string,
  "lastIncrementalRowTime": string,

  // Union field _incremental_row_count can be only one of the following:
  "incrementalRowCount": string
  // End of list of possible types for union field _incremental_row_count.
}
```

| Fields                                                                                            |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
|---------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `disabledReason`                                                                                  | `enum ( `[`DisabledReason`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.DisabledReason)` )` Output only. Reason why incremental query results are/were not written by the query.                                                                                                                                                                                                                                                                                                   |
| `disabledReasonDetails`                                                                           | `string` Output only. Additional human-readable clarification, if available, for DisabledReason.                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| `resultSetLastReplaceTime`                                                                        | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. The time at which the result table's contents were completely replaced. May be absent if no results have been written or the query has completed. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` . |
| `resultSetLastModifyTime`                                                                         | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. The time at which the result table's contents were modified. May be absent if no results have been written or the query has completed. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .            |
| `firstIncrementalRowTime`                                                                         | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. The time at which the first incremental result was written. If the query needed to restart internally, this only describes the final attempt. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .     |
| `lastIncrementalRowTime`                                                                          | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. The time at which the last incremental result was written. Does not include the final result written after query completion. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .                      |
| Union field `_incremental_row_count` . `_incremental_row_count` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| `incrementalRowCount`                                                                             | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Output only. Number of rows that were in the latest result set before query completion.                                                                                                                                                                                                                                                                                                                                                       |
|                                                                                                   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |

### GenAiStats

**JSON representation**

```
{
  "functionStats": [
    {
      object (GenAiFunctionStats)
    }
  ],

  // Union field _error_stats can be only one of the following:
  "errorStats": {
    object (GenAiErrorStats)
  }
  // End of list of possible types for union field _error_stats.
}
```

| Fields                                                                        |                                                                                                                                                                                                                                                                                                                            |
|-------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `functionStats[]`                                                             | `object ( `[`GenAiFunctionStats`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.GenAiFunctionStats)` )` Function level stats for GenAI Functions. For more information, see [Generative AI overview](https://docs.cloud.google.com/bigquery/docs/generative-ai-overview) . |
| Union field `_error_stats` . `_error_stats` can be only one of the following: |                                                                                                                                                                                                                                                                                                                            |
| `errorStats`                                                                  | `object ( `[`GenAiErrorStats`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.GenAiErrorStats)` )` Job level error stats across all GenAi functions                                                                                                                         |
|                                                                               |                                                                                                                                                                                                                                                                                                                            |

### GenAiErrorStats

**JSON representation**

```
{
  "errors": [
    string
  ]
}
```

| Fields     |                                                                                   |
|------------|-----------------------------------------------------------------------------------|
| `errors[]` | `string` A list of unique errors at query level (up to 5, truncated to 100 chars) |

### GenAiFunctionStats

**JSON representation**

```
{

  // Union field _function_name can be only one of the following:
  "functionName": string
  // End of list of possible types for union field _function_name.

  // Union field _prompt can be only one of the following:
  "prompt": string
  // End of list of possible types for union field _prompt.

  // Union field _num_processed_rows can be only one of the following:
  "numProcessedRows": string
  // End of list of possible types for union field _num_processed_rows.

  // Union field _error_stats can be only one of the following:
  "errorStats": {
    object (GenAiFunctionErrorStats)
  }
  // End of list of possible types for union field _error_stats.

  // Union field _cost_optimization_stats can be only one of the following:
  "costOptimizationStats": {
    object (GenAiFunctionCostOptimizationStats)
  }
  // End of list of possible types for union field _cost_optimization_stats.

  // Union field _cache_stats can be only one of the following:
  "cacheStats": {
    object (GenAiFunctionCacheStats)
  }
  // End of list of possible types for union field _cache_stats.
}
```

| Fields                                                                                                |                                                                                                                                                                                                                                                                   |
|-------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `_function_name` . `_function_name` can be only one of the following:                     |                                                                                                                                                                                                                                                                   |
| `functionName`                                                                                        | `string` Name of the function.                                                                                                                                                                                                                                    |
|                                                                                                       |                                                                                                                                                                                                                                                                   |
| Union field `_prompt` . `_prompt` can be only one of the following:                                   |                                                                                                                                                                                                                                                                   |
| `prompt`                                                                                              | `string` User input prompt of the function (truncated to 20 chars).                                                                                                                                                                                               |
|                                                                                                       |                                                                                                                                                                                                                                                                   |
| Union field `_num_processed_rows` . `_num_processed_rows` can be only one of the following:           |                                                                                                                                                                                                                                                                   |
| `numProcessedRows`                                                                                    | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Number of rows processed by this GenAi function. This includes all cost_optimized, llm_inferred and failed_rows.                                                           |
|                                                                                                       |                                                                                                                                                                                                                                                                   |
| Union field `_error_stats` . `_error_stats` can be only one of the following:                         |                                                                                                                                                                                                                                                                   |
| `errorStats`                                                                                          | `object ( `[`GenAiFunctionErrorStats`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.GenAiFunctionErrorStats)` )` Error stats for the function.                                                                   |
|                                                                                                       |                                                                                                                                                                                                                                                                   |
| Union field `_cost_optimization_stats` . `_cost_optimization_stats` can be only one of the following: |                                                                                                                                                                                                                                                                   |
| `costOptimizationStats`                                                                               | `object ( `[`GenAiFunctionCostOptimizationStats`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.GenAiFunctionCostOptimizationStats)` )` Cost optimization stats if applied on the rows processed by the function. |
|                                                                                                       |                                                                                                                                                                                                                                                                   |
| Union field `_cache_stats` . `_cache_stats` can be only one of the following:                         |                                                                                                                                                                                                                                                                   |
| `cacheStats`                                                                                          | `object ( `[`GenAiFunctionCacheStats`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.GenAiFunctionCacheStats)` )` Cache stats for the function.                                                                   |
|                                                                                                       |                                                                                                                                                                                                                                                                   |

### GenAiFunctionErrorStats

**JSON representation**

```
{
  "errors": [
    string
  ],
  "numFailedRows": string
}
```

| Fields          |                                                                                                                                        |
|-----------------|----------------------------------------------------------------------------------------------------------------------------------------|
| `errors[]`      | `string` A list of unique errors at function level (up to 5, truncated to 100 chars).                                                  |
| `numFailedRows` | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Number of failed rows processed by the function |

### GenAiFunctionCostOptimizationStats

**JSON representation**

```
{

  // Union field _num_cost_optimized_rows can be only one of the following:
  "numCostOptimizedRows": string
  // End of list of possible types for union field _num_cost_optimized_rows.

  // Union field _message can be only one of the following:
  "message": string
  // End of list of possible types for union field _message.
}
```

| Fields                                                                                                |                                                                                                                                             |
|-------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `_num_cost_optimized_rows` . `_num_cost_optimized_rows` can be only one of the following: |                                                                                                                                             |
| `numCostOptimizedRows`                                                                                | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Number of rows inferred via cost optimized workflow. |
|                                                                                                       |                                                                                                                                             |
| Union field `_message` . `_message` can be only one of the following:                                 |                                                                                                                                             |
| `message`                                                                                             | `string` System generated message to provide insights into cost optimization state.                                                         |
|                                                                                                       |                                                                                                                                             |

### GenAiFunctionCacheStats

**JSON representation**

```
{

  // Union field _num_cache_hit_rows can be only one of the following:
  "numCacheHitRows": string
  // End of list of possible types for union field _num_cache_hit_rows.
}
```

| Fields                                                                                      |                                                                                                                          |
|---------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------|
| Union field `_num_cache_hit_rows` . `_num_cache_hit_rows` can be only one of the following: |                                                                                                                          |
| `numCacheHitRows`                                                                           | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Number of rows served from cache. |
|                                                                                             |                                                                                                                          |

### ObjectStorageStats

**JSON representation**

```
{

  // Union field _cloud_provider can be only one of the following:
  "cloudProvider": enum (CloudProvider)
  // End of list of possible types for union field _cloud_provider.

  // Union field _object_storage_bytes_read can be only one of the following:
  "objectStorageBytesRead": string
  // End of list of possible types for union field _object_storage_bytes_read.

  // Union field _cache_bytes_read can be only one of the following:
  "cacheBytesRead": string
  // End of list of possible types for union field _cache_bytes_read.
}
```

| Fields                                                                                                    |                                                                                                                                                                                              |
|-----------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `_cloud_provider` . `_cloud_provider` can be only one of the following:                       |                                                                                                                                                                                              |
| `cloudProvider`                                                                                           | `enum ( `[`CloudProvider`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.CloudProvider)` )` The cloud provider for this block of statistics. |
|                                                                                                           |                                                                                                                                                                                              |
| Union field `_object_storage_bytes_read` . `_object_storage_bytes_read` can be only one of the following: |                                                                                                                                                                                              |
| `objectStorageBytesRead`                                                                                  | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Total bytes read directly from the cloud provider's storage.                                          |
|                                                                                                           |                                                                                                                                                                                              |
| Union field `_cache_bytes_read` . `_cache_bytes_read` can be only one of the following:                   |                                                                                                                                                                                              |
| `cacheBytesRead`                                                                                          | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Total bytes read from the GCP Lakehouse-internal cache, avoiding an object storage read.              |
|                                                                                                           |                                                                                                                                                                                              |

### JobStatistics3

**JSON representation**

```
{
  "inputFiles": string,
  "inputFileBytes": string,
  "outputRows": string,
  "outputBytes": string,
  "badRecords": string,
  "timeline": [
    {
      object (QueryTimelineSample)
    }
  ]
}
```

| Fields           |                                                                                                                                                                                                                                                                                                                                                                              |
|------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `inputFiles`     | `string ( `[`Int64Value`](https://developers.google.com/discovery/v1/type-format)` format)` Output only. Number of source files in a load job.                                                                                                                                                                                                                               |
| `inputFileBytes` | `string ( `[`Int64Value`](https://developers.google.com/discovery/v1/type-format)` format)` Output only. Number of bytes of source data in a load job.                                                                                                                                                                                                                       |
| `outputRows`     | `string ( `[`Int64Value`](https://developers.google.com/discovery/v1/type-format)` format)` Output only. Number of rows imported in a load job. Note that while an import job is in the running state, this value may change.                                                                                                                                                |
| `outputBytes`    | `string ( `[`Int64Value`](https://developers.google.com/discovery/v1/type-format)` format)` Output only. Size of the loaded data in bytes. Note that while a load job is in the running state, this value may change.                                                                                                                                                        |
| `badRecords`     | `string ( `[`Int64Value`](https://developers.google.com/discovery/v1/type-format)` format)` Output only. The number of bad records encountered. Note that if the job has failed because of more bad records encountered than the maximum allowed in the load job configuration, then this number can be less than the total number of bad records present in the input data. |
| `timeline[]`     | `object ( `[`QueryTimelineSample`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.QueryTimelineSample)` )` Output only. Describes a timeline of job execution.                                                                                                                                                                |

### JobStatistics4

**JSON representation**

```
{
  "destinationUriFileCounts": [
    string
  ],
  "inputBytes": string,
  "timeline": [
    {
      object (QueryTimelineSample)
    }
  ]
}
```

| Fields                       |                                                                                                                                                                                                                                                                                                                                        |
|------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `destinationUriFileCounts[]` | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Output only. Number of files per destination URI or URI pattern specified in the extract configuration. These values will be in the same order as the URIs specified in the 'destinationUris' field.                                            |
| `inputBytes`                 | `string ( `[`Int64Value`](https://developers.google.com/discovery/v1/type-format)` format)` Output only. Number of user bytes extracted into the result. This is the byte count as computed by BigQuery for billing purposes and doesn't have any relationship with the number of actual result bytes extracted in the desired format. |
| `timeline[]`                 | `object ( `[`QueryTimelineSample`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.QueryTimelineSample)` )` Output only. Describes a timeline of job execution.                                                                                                                          |

### CopyJobStatistics

**JSON representation**

```
{
  "copiedRows": string,
  "copiedLogicalBytes": string,
  "remoteDestinationRegion": string
}
```

| Fields                    |                                                                                                                                                                   |
|---------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `copiedRows`              | `string ( `[`Int64Value`](https://developers.google.com/discovery/v1/type-format)` format)` Output only. Number of rows copied to the destination table.          |
| `copiedLogicalBytes`      | `string ( `[`Int64Value`](https://developers.google.com/discovery/v1/type-format)` format)` Output only. Number of logical bytes copied to the destination table. |
| `remoteDestinationRegion` | `string` Output only. Destination region for a cross-region copy job. Not set for in-region copy jobs.                                                            |

### ScriptStatistics

**JSON representation**

```
{
  "evaluationKind": enum (EvaluationKind),
  "stackFrames": [
    {
      object (ScriptStackFrame)
    }
  ]
}
```

| Fields           |                                                                                                                                                                                                                                                                                                                                                         |
|------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `evaluationKind` | `enum ( `[`EvaluationKind`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.EvaluationKind)` )` Whether this child job was a statement or expression.                                                                                                                                                     |
| `stackFrames[]`  | `object ( `[`ScriptStackFrame`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.ScriptStackFrame)` )` Stack trace showing the line/column/procedure name of each frame on the stack at the point where the current evaluation happened. The leaf frame is first, the primary script is last. Never empty. |

### ScriptStackFrame

**JSON representation**

```
{
  "startLine": integer,
  "startColumn": integer,
  "endLine": integer,
  "endColumn": integer,
  "procedureId": string,
  "text": string
}
```

| Fields        |                                                                                     |
|---------------|-------------------------------------------------------------------------------------|
| `startLine`   | `integer` Output only. One-based start line.                                        |
| `startColumn` | `integer` Output only. One-based start column.                                      |
| `endLine`     | `integer` Output only. One-based end line.                                          |
| `endColumn`   | `integer` Output only. One-based end column.                                        |
| `procedureId` | `string` Output only. Name of the active procedure, empty if in a top-level script. |
| `text`        | `string` Output only. Text of the current statement/expression.                     |

### RowLevelSecurityStatistics

**JSON representation**

```
{
  "rowLevelSecurityApplied": boolean
}
```

| Fields                    |                                                                           |
|---------------------------|---------------------------------------------------------------------------|
| `rowLevelSecurityApplied` | `boolean` Whether any accessed data was protected by row access policies. |

### DataMaskingStatistics

**JSON representation**

```
{
  "dataMaskingApplied": boolean
}
```

| Fields               |                                                                        |
|----------------------|------------------------------------------------------------------------|
| `dataMaskingApplied` | `boolean` Whether any accessed data was protected by the data masking. |

### TransactionInfo

**JSON representation**

```
{
  "transactionId": string
}
```

| Fields          |                                                        |
|-----------------|--------------------------------------------------------|
| `transactionId` | `string` Output only. \[Alpha\] Id of the transaction. |

### SessionInfo

**JSON representation**

```
{
  "sessionId": string
}
```

| Fields      |                                              |
|-------------|----------------------------------------------|
| `sessionId` | `string` Output only. The id of the session. |

### JobStatus

**JSON representation**

```
{
  "errorResult": {
    object (ErrorProto)
  },
  "errors": [
    {
      object (ErrorProto)
    }
  ],
  "state": string
}
```

| Fields        |                                                                                                                                                                                                                                                                                                                                                                                               |
|---------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `errorResult` | `object ( `[`ErrorProto`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.ErrorProto)` )` Output only. Final error result of the job. If present, indicates that the job has completed and was unsuccessful.                                                                                                                                |
| `errors[]`    | `object ( `[`ErrorProto`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.ErrorProto)` )` Output only. The first errors encountered during the running of the job. The final message includes the number of errors that caused the process to stop. Errors here do not necessarily mean that the job has not completed or was unsuccessful. |
| `state`       | `string` Output only. Running state of the job. Valid states include 'PENDING', 'RUNNING', and 'DONE'.                                                                                                                                                                                                                                                                                        |

### ErrorProto

**JSON representation**

```
{
  "reason": string,
  "location": string,
  "debugInfo": string,
  "message": string
}
```

| Fields      |                                                                                             |
|-------------|---------------------------------------------------------------------------------------------|
| `reason`    | `string` A short error code that summarizes the error.                                      |
| `location`  | `string` Specifies where the error occurred, if present.                                    |
| `debugInfo` | `string` Debugging information. This property is internal to Google and should not be used. |
| `message`   | `string` A human-readable description of the error.                                         |

### JobCreationReason

**JSON representation**

```
{
  "code": enum (Code)
}
```

| Fields |                                                                                                                                                                                                 |
|--------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `code` | `enum ( `[`Code`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/cancel_job#Output.Schema.Code_3)` )` Output only. Specifies the high level reason why a Job was created. |

### FileSetSpecType

This enum defines how to interpret source URIs for load jobs and external tables.

| Enums                                            |                                                                                                                                            |
|--------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------|
| `FILE_SET_SPEC_TYPE_FILE_SYSTEM_MATCH`           | This option expands source URIs by listing files from the object store. It is the default behavior if FileSetSpecType is not set.          |
| `FILE_SET_SPEC_TYPE_NEW_LINE_DELIMITED_MANIFEST` | This option indicates that the provided URIs are newline-delimited manifest files, with one URI per line. Wildcard URIs are not supported. |

### RoundingMode

Rounding mode options that can be used when storing NUMERIC or BIGNUMERIC values.

| Enums                       |                                                                                                                                                                                                                                  |
|-----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `ROUNDING_MODE_UNSPECIFIED` | Unspecified will default to using ROUND_HALF_AWAY_FROM_ZERO.                                                                                                                                                                     |
| `ROUND_HALF_AWAY_FROM_ZERO` | ROUND_HALF_AWAY_FROM_ZERO rounds half values away from zero when applying precision and scale upon writing of NUMERIC and BIGNUMERIC values. For Scale: 0 1.1, 1.2, 1.3, 1.4 =\> 1 1.5, 1.6, 1.7, 1.8, 1.9 =\> 2                 |
| `ROUND_HALF_EVEN`           | ROUND_HALF_EVEN rounds half values to the nearest even value when applying precision and scale upon writing of NUMERIC and BIGNUMERIC values. For Scale: 0 1.1, 1.2, 1.3, 1.4 =\> 1 1.5 =\> 2 1.6, 1.7, 1.8, 1.9 =\> 2 2.5 =\> 2 |

### GeneratedMode

Dictates when system generated values are used to populate the field.

| Enums                        |                                                                                                  |
|------------------------------|--------------------------------------------------------------------------------------------------|
| `GENERATED_MODE_UNSPECIFIED` | Unspecified GeneratedMode will default to GENERATED_ALWAYS.                                      |
| `GENERATED_ALWAYS`           | Field can only have system generated values. Users cannot manually insert values into the field. |
| `GENERATED_BY_DEFAULT`       | Use system generated values only if the user does not explicitly provide a value.                |

### TypeSystem

External systems, such as query engines or table formats, that have their own data types.

| Enums                     |                             |
|---------------------------|-----------------------------|
| `TYPE_SYSTEM_UNSPECIFIED` | TypeSystem not specified.   |
| `HIVE`                    | Represents Hive data types. |

### DecimalTargetType

The data types that could be used as a target type when converting decimal values.

| Enums                             |                                                       |
|-----------------------------------|-------------------------------------------------------|
| `DECIMAL_TARGET_TYPE_UNSPECIFIED` | Invalid type.                                         |
| `NUMERIC`                         | Decimal values could be converted to NUMERIC type.    |
| `BIGNUMERIC`                      | Decimal values could be converted to BIGNUMERIC type. |
| `STRING`                          | Decimal values could be converted to STRING type.     |

### JsonExtension

Used to indicate that a JSON variant, rather than normal JSON, is being used as the source_format. This should only be used in combination with the JSON source format.

| Enums                        |                                                                                                                                                     |
|------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------|
| `JSON_EXTENSION_UNSPECIFIED` | The default if provided value is not one included in the enum, or the value is not specified. The source format is parsed without any modification. |
| `GEOJSON`                    | Use GeoJSON variant of JSON. See <https://tools.ietf.org/html/rfc7946> .                                                                            |

### MapTargetType

Indicates the map target type. Only applies to parquet maps.

| Enums                         |                                                                                                                          |
|-------------------------------|--------------------------------------------------------------------------------------------------------------------------|
| `MAP_TARGET_TYPE_UNSPECIFIED` | In this mode, the map will have the following schema: struct map_field_name { repeated struct key_value { key value } }. |
| `ARRAY_OF_STRUCT`             | In this mode, the map will have the following schema: repeated struct map_field_name { key value }.                      |

### ObjectMetadata

Supported Object Metadata Types.

| Enums                         |                               |
|-------------------------------|-------------------------------|
| `OBJECT_METADATA_UNSPECIFIED` | Unspecified by default.       |
| `DIRECTORY`                   | A synonym for `SIMPLE` .      |
| `SIMPLE`                      | Directory listing of objects. |

### MetadataCacheMode

MetadataCacheMode identifies if the table should use metadata caching for files from external source (eg Google Cloud Storage).

| Enums                             |                                                                                                                                                                                                      |
|-----------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `METADATA_CACHE_MODE_UNSPECIFIED` | Unspecified metadata cache mode.                                                                                                                                                                     |
| `AUTOMATIC`                       | Set this mode to trigger automatic background refresh of metadata cache from the external source. Queries will use the latest available cache version within the table's maxStaleness interval.      |
| `MANUAL`                          | Set this mode to enable triggering manual refresh of the metadata cache from external source. Queries will use the latest manually triggered cache version within the table's maxStaleness interval. |

### TypeKind

The kind of the datatype.

| Enums                   |                                                                                                                                    |
|-------------------------|------------------------------------------------------------------------------------------------------------------------------------|
| `TYPE_KIND_UNSPECIFIED` | Invalid type.                                                                                                                      |
| `INT64`                 | Encoded as a string in decimal format.                                                                                             |
| `BOOL`                  | Encoded as a boolean "false" or "true".                                                                                            |
| `FLOAT64`               | Encoded as a number, or string "NaN", "Infinity" or "-Infinity".                                                                   |
| `STRING`                | Encoded as a string value.                                                                                                         |
| `BYTES`                 | Encoded as a base64 string per RFC 4648, section 4.                                                                                |
| `TIMESTAMP`             | Encoded as an RFC 3339 timestamp with mandatory "Z" time zone string: 1985-04-12T23:20:50.52Z                                      |
| `DATE`                  | Encoded as RFC 3339 full-date format string: 1985-04-12                                                                            |
| `TIME`                  | Encoded as RFC 3339 partial-time format string: 23:20:50.52                                                                        |
| `DATETIME`              | Encoded as RFC 3339 full-date "T" partial-time: 1985-04-12T23:20:50.52                                                             |
| `INTERVAL`              | Encoded as fully qualified 3 part: 0-5 15 2:30:45.6                                                                                |
| `GEOGRAPHY`             | Encoded as WKT                                                                                                                     |
| `NUMERIC`               | Encoded as a decimal string.                                                                                                       |
| `BIGNUMERIC`            | Encoded as a decimal string.                                                                                                       |
| `JSON`                  | Encoded as a string.                                                                                                               |
| `ARRAY`                 | Encoded as a list with types matching Type.array_type.                                                                             |
| `STRUCT`                | Encoded as a list with fields of type Type.struct_type\[i\]. List is used because a JSON object cannot have duplicate field names. |
| `RANGE`                 | Encoded as a pair with types matching range_element_type. Pairs must begin with "\[", end with ")", and be separated by ", ".      |
| `UUID`                  | Encoded as a string.                                                                                                               |

### NullValue

Represents a JSON `null` .

`NullValue` is a sentinel, using an enum with only one value to represent the null value for the `Value` type union.

A field of type `NullValue` with any value other than `0` is considered invalid. Most ProtoJSON serializers will emit a `Value` with a `null_value` set as a JSON `null` regardless of the integer value, and so will round trip to a `0` value.

| Enums        |             |
|--------------|-------------|
| `NULL_VALUE` | Null value. |

### KeyResultStatementKind

KeyResultStatementKind controls how the key result is determined.

| Enums                                   |                                                       |
|-----------------------------------------|-------------------------------------------------------|
| `KEY_RESULT_STATEMENT_KIND_UNSPECIFIED` | Default value.                                        |
| `LAST`                                  | The last result determines the key result.            |
| `FIRST_SELECT`                          | The first SELECT statement determines the key result. |

### DeserializationOption

`DeserializationOption` defines the `TProtocol` implementation that will be used to deserialize Thrift data.

| Enums                                |                                                 |
|--------------------------------------|-------------------------------------------------|
| `DESERIALIZATION_OPTION_UNSPECIFIED` | Default value. This value is unused.            |
| `THRIFT_BINARY_PROTOCOL_OPTION`      | Use `TBinaryProtocol` to deserialize the data.. |

### FramingOption

Framing in Apache Thrift means 4 bytes added in front of the serialized record or data blocks to inidicate the size of the followed record or data block. Please see `TFramedTransport` for more details. One thing to note is that the 4-byte record size added by `TFramedTransport` is in big endian. A `TFramedTransport` framed block looks like:

\| 4-byte size (big endian) \| serialized record ... \|

We also support framing with little endian record or data block size.

| Enums                        |                                                                               |
|------------------------------|-------------------------------------------------------------------------------|
| `FRAMING_OPTION_UNSPECIFIED` | Default value. This value is unused.                                          |
| `NOT_FRAMED`                 | Records or data blocks are not framed.                                        |
| `FRAMED_WITH_BIG_ENDIAN`     | Records or data blocks are framed with a 4-byte record size in big endian.    |
| `FRAMED_WITH_LITTLE_ENDIAN`  | Records or data blocks are framed with a 4-byte record size in little endian. |

### ColumnNameCharacterMap

Indicates the character map used for column names.

| Enums                                   |                                                                                                                                         |
|-----------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------|
| `COLUMN_NAME_CHARACTER_MAP_UNSPECIFIED` | Unspecified column name character map.                                                                                                  |
| `STRICT`                                | Support flexible column name and reject invalid column names.                                                                           |
| `V1`                                    | Support alphanumeric + underscore characters and names must start with a letter or underscore. Invalid column names will be normalized. |
| `V2`                                    | Support flexible column name. Invalid column names will be normalized.                                                                  |

### SourceColumnMatch

Indicates the strategy used to match loaded columns to the schema.

| Enums                             |                                                                                                                                                                                                                         |
|-----------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `SOURCE_COLUMN_MATCH_UNSPECIFIED` | Uses sensible defaults based on how the schema is provided. If autodetect is used, then columns are matched by name. Otherwise, columns are matched by position. This is done to keep the behavior backward-compatible. |
| `POSITION`                        | Matches by position. This assumes that the columns are ordered the same way as the schema.                                                                                                                              |
| `NAME`                            | Matches by name. This reads the header row as column names and reorders columns to match the field names in the schema.                                                                                                 |

### OperationType

Indicates different operation types supported in table copy job.

| Enums                        |                                                                                           |
|------------------------------|-------------------------------------------------------------------------------------------|
| `OPERATION_TYPE_UNSPECIFIED` | Unspecified operation type.                                                               |
| `COPY`                       | The source and destination table have the same table type.                                |
| `SNAPSHOT`                   | The source table type is TABLE and the destination table type is SNAPSHOT.                |
| `RESTORE`                    | The source table type is SNAPSHOT and the destination table type is TABLE.                |
| `CLONE`                      | The source and destination table have the same table type, but only bill for unique data. |

### ComputeMode

Indicates the type of compute mode.

| Enums                      |                                                   |
|----------------------------|---------------------------------------------------|
| `COMPUTE_MODE_UNSPECIFIED` | ComputeMode type not specified.                   |
| `BIGQUERY`                 | This stage was processed using BigQuery slots.    |
| `BI_ENGINE`                | This stage was processed using BI Engine compute. |

### DmlMode

Enum to specify the DML mode used.

| Enums                  |                                      |
|------------------------|--------------------------------------|
| `DML_MODE_UNSPECIFIED` | Default value. This value is unused. |
| `COARSE_GRAINED_DML`   | Coarse-grained DML was used.         |
| `FINE_GRAINED_DML`     | Fine-grained DML was used.           |

### FineGrainedDmlUnusedReason

Reason for disabling fine-grained DML. Additional values may be added in the future.

| Enums                                        |                                                                                                                                                                            |
|----------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `FINE_GRAINED_DML_UNUSED_REASON_UNSPECIFIED` | Default value. This value is unused.                                                                                                                                       |
| `MAX_PARTITION_SIZE_EXCEEDED`                | Max partition size threshold exceeded. [Fine-grained DML Limitations](https://docs.cloud.google.com/bigquery/docs/data-manipulation-language#fine-grained-dml-limitations) |
| `TABLE_NOT_ENROLLED`                         | The table is not enrolled for fine-grained DML.                                                                                                                            |
| `DML_IN_MULTI_STATEMENT_TRANSACTION`         | The DML statement is part of a multi-statement transaction.                                                                                                                |

### SeasonalPeriodType

Seasonal period type.

| Enums                              |                                         |
|------------------------------------|-----------------------------------------|
| `SEASONAL_PERIOD_TYPE_UNSPECIFIED` | Unspecified seasonal period.            |
| `NO_SEASONALITY`                   | No seasonality                          |
| `DAILY`                            | Daily period, 24 hours.                 |
| `WEEKLY`                           | Weekly period, 7 days.                  |
| `MONTHLY`                          | Monthly period, 30 days or irregular.   |
| `QUARTERLY`                        | Quarterly period, 90 days or irregular. |
| `YEARLY`                           | Yearly period, 365 days or irregular.   |
| `HOURLY`                           | Hourly period, 1 hour.                  |

### ModelType

Indicates the type of the Model.

| Enums                            |                                                                                                                        |
|----------------------------------|------------------------------------------------------------------------------------------------------------------------|
| `MODEL_TYPE_UNSPECIFIED`         | Default value.                                                                                                         |
| `LINEAR_REGRESSION`              | Linear regression model.                                                                                               |
| `LOGISTIC_REGRESSION`            | Logistic regression based classification model.                                                                        |
| `KMEANS`                         | K-means clustering model.                                                                                              |
| `MATRIX_FACTORIZATION`           | Matrix factorization model.                                                                                            |
| `DNN_CLASSIFIER`                 | DNN classifier model.                                                                                                  |
| `TENSORFLOW`                     | An imported TensorFlow model.                                                                                          |
| `DNN_REGRESSOR`                  | DNN regressor model.                                                                                                   |
| `XGBOOST`                        | An imported XGBoost model.                                                                                             |
| `BOOSTED_TREE_REGRESSOR`         | Boosted tree regressor model.                                                                                          |
| `BOOSTED_TREE_CLASSIFIER`        | Boosted tree classifier model.                                                                                         |
| `ARIMA`                          | ARIMA model.                                                                                                           |
| `AUTOML_REGRESSOR`               | AutoML Tables regression model.                                                                                        |
| `AUTOML_CLASSIFIER`              | AutoML Tables classification model.                                                                                    |
| `PCA`                            | Prinpical Component Analysis model.                                                                                    |
| `DNN_LINEAR_COMBINED_CLASSIFIER` | Wide-and-deep classifier model.                                                                                        |
| `DNN_LINEAR_COMBINED_REGRESSOR`  | Wide-and-deep regressor model.                                                                                         |
| `AUTOENCODER`                    | Autoencoder model.                                                                                                     |
| `ARIMA_PLUS`                     | New name for the ARIMA model.                                                                                          |
| `ARIMA_PLUS_XREG`                | ARIMA with external regressors.                                                                                        |
| `RANDOM_FOREST_REGRESSOR`        | Random forest regressor model.                                                                                         |
| `RANDOM_FOREST_CLASSIFIER`       | Random forest classifier model.                                                                                        |
| `TENSORFLOW_LITE`                | An imported TensorFlow Lite model.                                                                                     |
| `ONNX`                           | An imported ONNX model.                                                                                                |
| `TRANSFORM_ONLY`                 | Model to capture the columns and logic in the TRANSFORM clause along with statistics useful for ML analytic functions. |
| `CONTRIBUTION_ANALYSIS`          | The contribution analysis model.                                                                                       |

### TrainingType

Training type.

| Enums                       |                                                                                                                                           |
|-----------------------------|-------------------------------------------------------------------------------------------------------------------------------------------|
| `TRAINING_TYPE_UNSPECIFIED` | Unspecified training type.                                                                                                                |
| `SINGLE_TRAINING`           | Single training with fixed parameter space.                                                                                               |
| `HPARAM_TUNING`             | [Hyperparameter tuning training](https://cloud.google.com/bigquery-ml/docs/reference/standard-sql/bigqueryml-syntax-hp-tuning-overview) . |

### LossType

Loss metric to evaluate model training performance.

| Enums                   |                                                |
|-------------------------|------------------------------------------------|
| `LOSS_TYPE_UNSPECIFIED` | Default value.                                 |
| `MEAN_SQUARED_LOSS`     | Mean squared loss, used for linear regression. |
| `MEAN_LOG_LOSS`         | Mean log loss, used for logistic regression.   |

### DataSplitMethod

Indicates the method to split input data into multiple tables.

| Enums                           |                                                                                            |
|---------------------------------|--------------------------------------------------------------------------------------------|
| `DATA_SPLIT_METHOD_UNSPECIFIED` | Default value.                                                                             |
| `RANDOM`                        | Splits data randomly.                                                                      |
| `CUSTOM`                        | Splits data with the user provided tags.                                                   |
| `SEQUENTIAL`                    | Splits data sequentially.                                                                  |
| `NO_SPLIT`                      | Data split will be skipped.                                                                |
| `AUTO_SPLIT`                    | Splits data automatically: Uses NO_SPLIT if the data size is small. Otherwise uses RANDOM. |

### LearnRateStrategy

Indicates the learning rate optimization strategy to use.

| Enums                             |                                             |
|-----------------------------------|---------------------------------------------|
| `LEARN_RATE_STRATEGY_UNSPECIFIED` | Default value.                              |
| `LINE_SEARCH`                     | Use line search to determine learning rate. |
| `CONSTANT`                        | Use a constant learning rate.               |

### DistanceType

Distance metric used to compute the distance between two points.

| Enums                       |                     |
|-----------------------------|---------------------|
| `DISTANCE_TYPE_UNSPECIFIED` | Default value.      |
| `EUCLIDEAN`                 | Eculidean distance. |
| `COSINE`                    | Cosine distance.    |

### OptimizationStrategy

Indicates the optimization strategy used for training.

| Enums                               |                                                            |
|-------------------------------------|------------------------------------------------------------|
| `OPTIMIZATION_STRATEGY_UNSPECIFIED` | Default value.                                             |
| `BATCH_GRADIENT_DESCENT`            | Uses an iterative batch gradient descent algorithm.        |
| `NORMAL_EQUATION`                   | Uses a normal equation to solve linear regression problem. |

### BoosterType

Booster types supported. Refer to booster parameter in XGBoost.

| Enums                      |                           |
|----------------------------|---------------------------|
| `BOOSTER_TYPE_UNSPECIFIED` | Unspecified booster type. |
| `GBTREE`                   | Gbtree booster.           |
| `DART`                     | Dart booster.             |

### DartNormalizeType

Type of normalization algorithm for boosted tree models using dart booster. Refer to normalize_type in XGBoost.

| Enums                             |                                                          |
|-----------------------------------|----------------------------------------------------------|
| `DART_NORMALIZE_TYPE_UNSPECIFIED` | Unspecified dart normalize type.                         |
| `TREE`                            | New trees have the same weight of each of dropped trees. |
| `FOREST`                          | New trees have the same weight of sum of dropped trees.  |

### TreeMethod

Tree construction algorithm used in boosted tree models. Refer to tree_method in XGBoost.

| Enums                     |                                                                            |
|---------------------------|----------------------------------------------------------------------------|
| `TREE_METHOD_UNSPECIFIED` | Unspecified tree method.                                                   |
| `AUTO`                    | Use heuristic to choose the fastest method.                                |
| `EXACT`                   | Exact greedy algorithm.                                                    |
| `APPROX`                  | Approximate greedy algorithm using quantile sketch and gradient histogram. |
| `HIST`                    | Fast histogram optimized approximate greedy algorithm.                     |

### FeedbackType

Indicates the training algorithm to use for matrix factorization models.

| Enums                       |                                                     |
|-----------------------------|-----------------------------------------------------|
| `FEEDBACK_TYPE_UNSPECIFIED` | Default value.                                      |
| `IMPLICIT`                  | Use weighted-als for implicit feedback problems.    |
| `EXPLICIT`                  | Use nonweighted-als for explicit feedback problems. |

### KmeansInitializationMethod

Indicates the method used to initialize the centroids for KMeans clustering algorithm.

| Enums                                      |                                                                                 |
|--------------------------------------------|---------------------------------------------------------------------------------|
| `KMEANS_INITIALIZATION_METHOD_UNSPECIFIED` | Unspecified initialization method.                                              |
| `RANDOM`                                   | Initializes the centroids randomly.                                             |
| `CUSTOM`                                   | Initializes the centroids using data specified in kmeans_initialization_column. |
| `KMEANS_PLUS_PLUS`                         | Initializes with kmeans++.                                                      |

### DataFrequency

Type of supported data frequency for time series forecasting models.

| Enums                        |                                         |
|------------------------------|-----------------------------------------|
| `DATA_FREQUENCY_UNSPECIFIED` | Default value.                          |
| `AUTO_FREQUENCY`             | Automatically inferred from timestamps. |
| `YEARLY`                     | Yearly data.                            |
| `QUARTERLY`                  | Quarterly data.                         |
| `MONTHLY`                    | Monthly data.                           |
| `WEEKLY`                     | Weekly data.                            |
| `DAILY`                      | Daily data.                             |
| `HOURLY`                     | Hourly data.                            |
| `PER_MINUTE`                 | Per-minute data.                        |

### HolidayRegion

Type of supported holiday regions for time series forecasting models.

| Enums                        |                                                                                  |
|------------------------------|----------------------------------------------------------------------------------|
| `HOLIDAY_REGION_UNSPECIFIED` | Holiday region unspecified.                                                      |
| `GLOBAL`                     | Global.                                                                          |
| `NA`                         | North America.                                                                   |
| `JAPAC`                      | Japan and Asia Pacific: Korea, Greater China, India, Australia, and New Zealand. |
| `EMEA`                       | Europe, the Middle East and Africa.                                              |
| `LAC`                        | Latin America and the Caribbean.                                                 |
| `AE`                         | United Arab Emirates                                                             |
| `AR`                         | Argentina                                                                        |
| `AT`                         | Austria                                                                          |
| `AU`                         | Australia                                                                        |
| `BE`                         | Belgium                                                                          |
| `BR`                         | Brazil                                                                           |
| `CA`                         | Canada                                                                           |
| `CH`                         | Switzerland                                                                      |
| `CL`                         | Chile                                                                            |
| `CN`                         | China                                                                            |
| `CO`                         | Colombia                                                                         |
| `CS`                         | Czechoslovakia                                                                   |
| `CZ`                         | Czech Republic                                                                   |
| `DE`                         | Germany                                                                          |
| `DK`                         | Denmark                                                                          |
| `DZ`                         | Algeria                                                                          |
| `EC`                         | Ecuador                                                                          |
| `EE`                         | Estonia                                                                          |
| `EG`                         | Egypt                                                                            |
| `ES`                         | Spain                                                                            |
| `FI`                         | Finland                                                                          |
| `FR`                         | France                                                                           |
| `GB`                         | Great Britain (United Kingdom)                                                   |
| `GR`                         | Greece                                                                           |
| `HK`                         | Hong Kong                                                                        |
| `HU`                         | Hungary                                                                          |
| `ID`                         | Indonesia                                                                        |
| `IE`                         | Ireland                                                                          |
| `IL`                         | Israel                                                                           |
| `IN`                         | India                                                                            |
| `IR`                         | Iran                                                                             |
| `IT`                         | Italy                                                                            |
| `JP`                         | Japan                                                                            |
| `KR`                         | Korea (South)                                                                    |
| `LV`                         | Latvia                                                                           |
| `MA`                         | Morocco                                                                          |
| `MX`                         | Mexico                                                                           |
| `MY`                         | Malaysia                                                                         |
| `NG`                         | Nigeria                                                                          |
| `NL`                         | Netherlands                                                                      |
| `NO`                         | Norway                                                                           |
| `NZ`                         | New Zealand                                                                      |
| `PE`                         | Peru                                                                             |
| `PH`                         | Philippines                                                                      |
| `PK`                         | Pakistan                                                                         |
| `PL`                         | Poland                                                                           |
| `PT`                         | Portugal                                                                         |
| `RO`                         | Romania                                                                          |
| `RS`                         | Serbia                                                                           |
| `RU`                         | Russian Federation                                                               |
| `SA`                         | Saudi Arabia                                                                     |
| `SE`                         | Sweden                                                                           |
| `SG`                         | Singapore                                                                        |
| `SI`                         | Slovenia                                                                         |
| `SK`                         | Slovakia                                                                         |
| `TH`                         | Thailand                                                                         |
| `TR`                         | Turkey                                                                           |
| `TW`                         | Taiwan                                                                           |
| `UA`                         | Ukraine                                                                          |
| `US`                         | United States                                                                    |
| `VE`                         | Venezuela                                                                        |
| `VN`                         | Vietnam                                                                          |
| `ZA`                         | South Africa                                                                     |

### HparamTuningObjective

Available evaluation metrics used as hyperparameter tuning objectives.

| Enums                                   |                                                                                                                                                                                      |
|-----------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `HPARAM_TUNING_OBJECTIVE_UNSPECIFIED`   | Unspecified evaluation metric.                                                                                                                                                       |
| `MEAN_ABSOLUTE_ERROR`                   | Mean absolute error. mean_absolute_error = AVG(ABS(label - predicted))                                                                                                               |
| `MEAN_SQUARED_ERROR`                    | Mean squared error. mean_squared_error = AVG(POW(label - predicted, 2))                                                                                                              |
| `MEAN_SQUARED_LOG_ERROR`                | Mean squared log error. mean_squared_log_error = AVG(POW(LN(1 + label) - LN(1 + predicted), 2))                                                                                      |
| `MEDIAN_ABSOLUTE_ERROR`                 | Mean absolute error. median_absolute_error = APPROX_QUANTILES(absolute_error, 2)\[OFFSET(1)\]                                                                                        |
| `R_SQUARED`                             | R^2 score. This corresponds to r2_score in ML.EVALUATE. r_squared = 1 - SUM(squared_error)/(COUNT(label)\*VAR_POP(label))                                                            |
| `EXPLAINED_VARIANCE`                    | Explained variance. explained_variance = 1 - VAR_POP(label_error)/VAR_POP(label)                                                                                                     |
| `PRECISION`                             | Precision is the fraction of actual positive predictions that had positive actual labels. For multiclass this is a macro-averaged metric treating each class as a binary classifier. |
| `RECALL`                                | Recall is the fraction of actual positive labels that were given a positive prediction. For multiclass this is a macro-averaged metric.                                              |
| `ACCURACY`                              | Accuracy is the fraction of predictions given the correct label. For multiclass this is a globally micro-averaged metric.                                                            |
| `F1_SCORE`                              | The F1 score is an average of recall and precision. For multiclass this is a macro-averaged metric.                                                                                  |
| `LOG_LOSS`                              | Logarithmic Loss. For multiclass this is a macro-averaged metric.                                                                                                                    |
| `ROC_AUC`                               | Area Under an ROC Curve. For multiclass this is a macro-averaged metric.                                                                                                             |
| `DAVIES_BOULDIN_INDEX`                  | Davies-Bouldin Index.                                                                                                                                                                |
| `MEAN_AVERAGE_PRECISION`                | Mean Average Precision.                                                                                                                                                              |
| `NORMALIZED_DISCOUNTED_CUMULATIVE_GAIN` | Normalized Discounted Cumulative Gain.                                                                                                                                               |
| `AVERAGE_RANK`                          | Average Rank.                                                                                                                                                                        |

### EncodingMethod

Supported encoding methods for categorical features.

| Enums                         |                              |
|-------------------------------|------------------------------|
| `ENCODING_METHOD_UNSPECIFIED` | Unspecified encoding method. |
| `ONE_HOT_ENCODING`            | Applies one-hot encoding.    |
| `LABEL_ENCODING`              | Applies label encoding.      |
| `DUMMY_ENCODING`              | Applies dummy encoding.      |

### ColorSpace

Enums for color space, used for processing images in Object Table. See more details at <https://www.tensorflow.org/io/tutorials/colorspace> .

| Enums                     |                         |
|---------------------------|-------------------------|
| `COLOR_SPACE_UNSPECIFIED` | Unspecified color space |
| `RGB`                     | RGB                     |
| `HSV`                     | HSV                     |
| `YIQ`                     | YIQ                     |
| `YUV`                     | YUV                     |
| `GRAYSCALE`               | GRAYSCALE               |

### PcaSolver

Enums for supported PCA solvers.

| Enums         |                          |
|---------------|--------------------------|
| `UNSPECIFIED` | Default value.           |
| `FULL`        | Full eigen-decoposition. |
| `RANDOMIZED`  | Randomized SVD.          |
| `AUTO`        | Auto.                    |

### ModelRegistry

Enums for supported model registries.

| Enums                        |                |
|------------------------------|----------------|
| `MODEL_REGISTRY_UNSPECIFIED` | Default value. |
| `VERTEX_AI`                  | Vertex AI.     |

### ReservationAffinityType

Supported reservation affinity types to configure a Vertex AI resource.

| Enums                                   |                       |
|-----------------------------------------|-----------------------|
| `RESERVATION_AFFINITY_TYPE_UNSPECIFIED` | Default value.        |
| `NO_RESERVATION`                        | No reservation.       |
| `ANY_RESERVATION`                       | Any reservation.      |
| `SPECIFIC_RESERVATION`                  | Specific reservation. |

### TrialStatus

Current status of the trial.

| Enums                      |                                                    |
|----------------------------|----------------------------------------------------|
| `TRIAL_STATUS_UNSPECIFIED` | Default value.                                     |
| `NOT_STARTED`              | Scheduled but not started.                         |
| `RUNNING`                  | Running state.                                     |
| `SUCCEEDED`                | The trial succeeded.                               |
| `FAILED`                   | The trial failed.                                  |
| `INFEASIBLE`               | The trial is infeasible due to the invalid params. |
| `STOPPED_EARLY`            | Trial stopped early because it's not promising.    |

### BiEngineMode

Indicates the type of BI Engine acceleration.

| Enums                           |                                                                                                                           |
|---------------------------------|---------------------------------------------------------------------------------------------------------------------------|
| `ACCELERATION_MODE_UNSPECIFIED` | BiEngineMode type not specified.                                                                                          |
| `DISABLED`                      | BI Engine disabled the acceleration. bi_engine_reasons specifies a more detailed reason.                                  |
| `PARTIAL`                       | Part of the query was accelerated using BI Engine. See bi_engine_reasons for why parts of the query were not accelerated. |
| `FULL`                          | All of the query was accelerated using BI Engine.                                                                         |

### BiEngineAccelerationMode

Indicates the type of BI Engine acceleration.

| Enums                                     |                                                                                                                      |
|-------------------------------------------|----------------------------------------------------------------------------------------------------------------------|
| `BI_ENGINE_ACCELERATION_MODE_UNSPECIFIED` | BiEngineMode type not specified.                                                                                     |
| `BI_ENGINE_DISABLED`                      | BI Engine acceleration was attempted but disabled. bi_engine_reasons specifies a more detailed reason.               |
| `PARTIAL_INPUT`                           | Some inputs were accelerated using BI Engine. See bi_engine_reasons for why parts of the query were not accelerated. |
| `FULL_INPUT`                              | All of the query inputs were accelerated using BI Engine.                                                            |
| `FULL_QUERY`                              | All of the query was accelerated using BI Engine.                                                                    |

### Code

Indicates the high-level reason for no/partial acceleration

| Enums                      |                                                                          |
|----------------------------|--------------------------------------------------------------------------|
| `CODE_UNSPECIFIED`         | BiEngineReason not specified.                                            |
| `NO_RESERVATION`           | No reservation available for BI Engine acceleration.                     |
| `INSUFFICIENT_RESERVATION` | Not enough memory available for BI Engine acceleration.                  |
| `UNSUPPORTED_SQL_TEXT`     | This particular SQL text is not supported for acceleration by BI Engine. |
| `INPUT_TOO_LARGE`          | Input too large for acceleration by BI Engine.                           |
| `OTHER_REASON`             | Catch-all code for all other cases for partial or disabled acceleration. |
| `TABLE_EXCLUDED`           | One or more tables were not eligible for BI Engine acceleration.         |

### IndexUsageMode

Indicates the type of search index usage in the entire search query. In this context, "usage" means that an index lookup is attempted to prune base table data, with effectiveness depending on the selectivity of the search term.

| Enums                          |                                                                                                                                                                                                                            |
|--------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `INDEX_USAGE_MODE_UNSPECIFIED` | Index usage mode not specified.                                                                                                                                                                                            |
| `UNUSED`                       | No search indexes were used in the search query. See [`indexUnusedReasons`](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/Job#IndexUnusedReason) for detailed reasons.                                     |
| `PARTIALLY_USED`               | Part of the search query used search indexes. See [`indexUnusedReasons`](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/Job#IndexUnusedReason) for why other parts of the query did not use search indexes. |
| `FULLY_USED`                   | The entire search query used search indexes.                                                                                                                                                                               |

### Code

Indicates the high-level reason for the scenario when no search index was used.

| Enums                                 |                                                                                                                                                                                                                                                                                                                        |
|---------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `CODE_UNSPECIFIED`                    | Code not specified.                                                                                                                                                                                                                                                                                                    |
| `INDEX_CONFIG_NOT_AVAILABLE`          | Indicates the search index configuration has not been created.                                                                                                                                                                                                                                                         |
| `PENDING_INDEX_CREATION`              | Indicates the search index creation has not been completed.                                                                                                                                                                                                                                                            |
| `BASE_TABLE_TRUNCATED`                | Indicates the base table has been truncated (rows have been removed from table with TRUNCATE TABLE statement) since the last time the search index was refreshed.                                                                                                                                                      |
| `INDEX_CONFIG_MODIFIED`               | Indicates the search index configuration has been changed since the last time the search index was refreshed.                                                                                                                                                                                                          |
| `TIME_TRAVEL_QUERY`                   | Indicates the search query accesses data at a timestamp before the last time the search index was refreshed.                                                                                                                                                                                                           |
| `NO_PRUNING_POWER`                    | Indicates the usage of search index will not contribute to any pruning improvement for the search function, e.g. when the search predicate is in a disjunction with other non-search predicates.                                                                                                                       |
| `UNINDEXED_SEARCH_FIELDS`             | Indicates the search index does not cover all fields in the search function.                                                                                                                                                                                                                                           |
| `UNSUPPORTED_SEARCH_PATTERN`          | Indicates the search index does not support the given search query pattern.                                                                                                                                                                                                                                            |
| `OPTIMIZED_WITH_MATERIALIZED_VIEW`    | Indicates the query has been optimized by using a materialized view.                                                                                                                                                                                                                                                   |
| `SECURED_BY_DATA_MASKING`             | Indicates the query has been secured by data masking, and thus search indexes are not applicable.                                                                                                                                                                                                                      |
| `MISMATCHED_TEXT_ANALYZER`            | Indicates that the search index and the search function call do not have the same text analyzer.                                                                                                                                                                                                                       |
| `BASE_TABLE_TOO_SMALL`                | Indicates the base table is too small (below a certain threshold). The index does not provide noticeable search performance gains when the base table is too small.                                                                                                                                                    |
| `BASE_TABLE_TOO_LARGE`                | Indicates that the total size of indexed base tables in your organization exceeds your region's limit and the index is not used in the query. To index larger base tables, you can [use your own reservation](https://cloud.google.com/bigquery/docs/search-index#use_your_own_reservation) for index-management jobs. |
| `ESTIMATED_PERFORMANCE_GAIN_TOO_LOW`  | Indicates that the estimated performance gain from using the search index is too low for the given search query.                                                                                                                                                                                                       |
| `COLUMN_METADATA_INDEX_NOT_USED`      | Indicates that the column metadata index (which the search index depends on) is not used. User can refer to the [column metadata index usage](https://cloud.google.com/bigquery/docs/metadata-indexing-managed-tables#view_column_metadata_index_usage) for more details on why it was not used.                       |
| `NOT_SUPPORTED_IN_STANDARD_EDITION`   | Indicates that search indexes can not be used for search query with STANDARD edition.                                                                                                                                                                                                                                  |
| `INDEX_SUPPRESSED_BY_FUNCTION_OPTION` | Indicates that an option in the search function that cannot make use of the index has been selected.                                                                                                                                                                                                                   |
| `QUERY_CACHE_HIT`                     | Indicates that the query was cached, and thus the search index was not used.                                                                                                                                                                                                                                           |
| `STALE_INDEX`                         | The index cannot be used in the search query because it is stale.                                                                                                                                                                                                                                                      |
| `INTERNAL_ERROR`                      | Indicates an internal error that causes the search index to be unused.                                                                                                                                                                                                                                                 |
| `OTHER_REASON`                        | Indicates that the reason search indexes cannot be used in the query is not covered by any of the other IndexUnusedReason options.                                                                                                                                                                                     |

### IndexUsageMode

Indicates the type of vector index usage in the entire vector search query.

| Enums                          |                                                                                                                                                                                                                                   |
|--------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `INDEX_USAGE_MODE_UNSPECIFIED` | Index usage mode not specified.                                                                                                                                                                                                   |
| `UNUSED`                       | No vector indexes were used in the vector search query. See [`indexUnusedReasons`](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/Job#IndexUnusedReason) for detailed reasons.                                     |
| `PARTIALLY_USED`               | Part of the vector search query used vector indexes. See [`indexUnusedReasons`](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/Job#IndexUnusedReason) for why other parts of the query did not use vector indexes. |
| `FULLY_USED`                   | The entire vector search query used vector indexes.                                                                                                                                                                               |

### Code

Indicates the high-level reason for the scenario when stored columns cannot be used in the query.

| Enums                               |                                                                                                                                            |
|-------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------|
| `CODE_UNSPECIFIED`                  | Default value.                                                                                                                             |
| `STORED_COLUMNS_COVER_INSUFFICIENT` | If stored columns do not fully cover the columns.                                                                                          |
| `BASE_TABLE_HAS_RLS`                | If the base table has RLS (Row Level Security).                                                                                            |
| `BASE_TABLE_HAS_CLS`                | If the base table has CLS (Column Level Security).                                                                                         |
| `UNSUPPORTED_PREFILTER`             | If the provided prefilter is not supported.                                                                                                |
| `INTERNAL_ERROR`                    | If an internal error is preventing stored columns from being used.                                                                         |
| `OTHER_REASON`                      | Indicates that the reason stored columns cannot be used in the query is not covered by any of the other StoredColumnsUnusedReason options. |

### RejectedReason

Reason why a materialized view was not chosen for a query. For more information, see [Understand why materialized views were rejected](https://cloud.google.com/bigquery/docs/materialized-views-use#understand-rejected) .

| Enums                                     |                                                                                                                                                                                                                                                                                                                     |
|-------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `REJECTED_REASON_UNSPECIFIED`             | Default unspecified value.                                                                                                                                                                                                                                                                                          |
| `NO_DATA`                                 | View has no cached data because it has not refreshed yet.                                                                                                                                                                                                                                                           |
| `COST`                                    | The estimated cost of the view is more expensive than another view or the base table. Note: The estimate cost might not match the billed cost.                                                                                                                                                                      |
| `BASE_TABLE_TRUNCATED`                    | View has no cached data because a base table is truncated.                                                                                                                                                                                                                                                          |
| `BASE_TABLE_DATA_CHANGE`                  | View is invalidated because of a data change in one or more base tables. It could be any recent change if the [`maxStaleness`](https://cloud.google.com/bigquery/docs/reference/rest/v2/tables#Table.FIELDS.max_staleness) option is not set for the view, or otherwise any change outside of the staleness window. |
| `BASE_TABLE_PARTITION_EXPIRATION_CHANGE`  | View is invalidated because a base table's partition expiration has changed.                                                                                                                                                                                                                                        |
| `BASE_TABLE_EXPIRED_PARTITION`            | View is invalidated because a base table's partition has expired.                                                                                                                                                                                                                                                   |
| `BASE_TABLE_INCOMPATIBLE_METADATA_CHANGE` | View is invalidated because a base table has an incompatible metadata change.                                                                                                                                                                                                                                       |
| `TIME_ZONE`                               | View is invalidated because it was refreshed with a time zone other than that of the current job.                                                                                                                                                                                                                   |
| `OUT_OF_TIME_TRAVEL_WINDOW`               | View is outside the time travel window.                                                                                                                                                                                                                                                                             |
| `BASE_TABLE_FINE_GRAINED_SECURITY_POLICY` | View is inaccessible to the user because of a fine-grained security policy on one of its base tables.                                                                                                                                                                                                               |
| `BASE_TABLE_TOO_STALE`                    | One of the view's base tables is too stale. For example, the cached metadata of a BigLake external table needs to be updated.                                                                                                                                                                                       |

### UnusedReason

Reasons for not using metadata caching.

| Enums                          |                                                                                                                                                                                                        |
|--------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `UNUSED_REASON_UNSPECIFIED`    | Unused reasons not specified.                                                                                                                                                                          |
| `EXCEEDED_MAX_STALENESS`       | Metadata cache was outside the table's maxStaleness.                                                                                                                                                   |
| `METADATA_CACHING_NOT_ENABLED` | Metadata caching feature is not enabled. [Update BigLake tables](https://docs.cloud.google.com/bigquery/docs/create-cloud-storage-table-biglake#update-biglake-tables) to enable the metadata caching. |
| `OTHER_REASON`                 | Other unknown reason.                                                                                                                                                                                  |

### DisabledReason

Reason why incremental query results are/were not written by the query.

| Enums                         |                                                                                                              |
|-------------------------------|--------------------------------------------------------------------------------------------------------------|
| `DISABLED_REASON_UNSPECIFIED` | Disabled reason not specified.                                                                               |
| `OTHER`                       | Incremental results are/were disabled for reasons not covered by the other enum values, e.g. runtime issues. |
| `UNSUPPORTED_OPERATOR`        | Query includes an operation that is not supported.                                                           |

### CloudProvider

The cloud provider hosting the object storage.

| Enums                        |                             |
|------------------------------|-----------------------------|
| `CLOUD_PROVIDER_UNSPECIFIED` | Unspecified cloud provider. |
| `GCP`                        | Google Cloud Platform.      |
| `AWS`                        | Amazon Web Services.        |
| `AZURE`                      | Microsoft Azure.            |

### EvaluationKind

Describes how the job is evaluated.

| Enums                         |                                                                   |
|-------------------------------|-------------------------------------------------------------------|
| `EVALUATION_KIND_UNSPECIFIED` | Default value.                                                    |
| `STATEMENT`                   | The statement appears directly in the script.                     |
| `EXPRESSION`                  | The statement evaluates an expression that appears in the script. |

### ReservationEdition

The type of editions. Different features and behaviors are provided to different editions Capacity commitments and reservations are linked to editions.

| Enums                             |                                                     |
|-----------------------------------|-----------------------------------------------------|
| `RESERVATION_EDITION_UNSPECIFIED` | Default value, which will be treated as ENTERPRISE. |
| `STANDARD`                        | Standard edition.                                   |
| `ENTERPRISE`                      | Enterprise edition.                                 |
| `ENTERPRISE_PLUS`                 | Enterprise Plus edition.                            |

### Code

Indicates the high level reason why a job was created.

| Enums              |                                                                                                                                                                                                                                                                                      |
|--------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `CODE_UNSPECIFIED` | Reason is not specified.                                                                                                                                                                                                                                                             |
| `REQUESTED`        | Job creation was requested.                                                                                                                                                                                                                                                          |
| `LONG_RUNNING`     | The query request ran beyond a system defined timeout specified by the [timeoutMs field in the QueryRequest](https://cloud.google.com/bigquery/docs/reference/rest/v2/jobs/query#queryrequest) . As a result it was considered a long running operation for which a job was created. |
| `LARGE_RESULTS`    | The results from the query cannot fit in the response.                                                                                                                                                                                                                               |
| `OTHER`            | BigQuery has determined that the query needs to be executed as a Job.                                                                                                                                                                                                                |

### Tool Annotations

[Tool annotations](https://modelcontextprotocol.io/specification/latest/schema#toolannotations) are sent to MCP clients to describe the basic risk of a given tool. Most clients treat these hints as untrusted, but they can be used to decide when a confirmation prompt might be sent to a user.

Along with the title string, the following boolean hints are defined as follows:

- `readOnlyHint` : If true, the tool doesn't modify its environment. Default: false.
- `destructiveHint` : If true, then the tool can perform destructive actions. If false, then the tool can only perform additive actions. Default: true.
- `idempotentHint` : If true, then calling the tool repeatedly with the same arguments will have no additional effect on its environment. Default: false.
- `openWorldHint` : If true, then the tool can interact with an 'open world' of external entities. If false, then the tool can only interact with internal entities. For example, a web search tool would be open world, while a memory tool would not be open world.

Destructive Hint: ❌ \| Idempotent Hint: ✅ \| Read Only Hint: ✅ \| Open World Hint: ❌
