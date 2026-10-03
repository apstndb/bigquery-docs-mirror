---
name: documents/docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/execute_sql
uri: https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/execute_sql
title: 'MCP Tools Reference: bigquery.googleapis.com'
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

## Tool: `execute_sql`

Run a SQL query in the project and return the result. Prefer the `execute_sql_readonly` tool if possible.

This tool can execute any query that bigquery supports including:

- SQL Queries ( `SELECT` , `INSERT` , `UPDATE` , `DELETE` , `CREATE` , etc.)
- AI/ML functions like `AI.FORECAST` , `AI.KEY_DRIVERS` , `ML.EVALUATE` , `ML.PREDICT`
- Any other query that bigquery supports.

Example Queries:

```sql
-- Insert data into a table.
        INSERT INTO `my_project.my_dataset`.my_table (name, age)
        VALUES ('Alice', 30);

        -- Create a table.
        CREATE TABLE `my_project.my_dataset`.my_table (
          name STRING,
          age INT64);

        -- DELETE data from a table.
        DELETE FROM `my_project.my_dataset`.my_table WHERE name = 'Alice';

        -- Create Dataset
        CREATE SCHEMA `my_project.my_dataset` OPTIONS (location = 'US');

        -- Drop table
        DROP TABLE `my_project.my_dataset`.my_table;

        -- Drop dataset
        DROP SCHEMA `my_project.my_dataset`;

        -- Create Model
        CREATE OR REPLACE MODEL `my_project.my_dataset.my_model`
        OPTIONS (
          model_type = 'LINEAR_REG'
          LS_INIT_LEARN_RATE=0.15,
          L1_REG=1,
          MAX_ITERATIONS=5,
          DATA_SPLIT_METHOD='SEQ',
          DATA_SPLIT_EVAL_FRACTION=0.3,
          DATA_SPLIT_COL='timestamp') AS
        SELECT col1, col2, timestamp, label FROM `my_project.my_dataset.my_table`;
        
```

Queries executed using the `execute_sql` tool will always have the default job label `goog-mcp-server: true` automatically set in addition to any custom `labels` provided in the request. Queries are charged to the project specified in the `project_id` field.

Query Execution Behavior: \* If the query completes within the synchronous timeout (default 20 seconds or custom `timeout_ms` ), the tool returns `job_complete: true` and the initial result rows directly. For fast queries, `job_id` may be omitted as no persistent background job is created; no further action or polling is needed. \* If the query takes longer than `timeout_ms` , the tool returns `job_complete: false` and a `job_id` . In this case, use the `get_query_results` tool with `job_id` to poll until `job_complete: true` , or use `cancel_job` to abort the running query. \* You can optionally specify `timeout_ms` to configure the maximum synchronous wait time in milliseconds (defaults to 20,000 ms), and `job_timeout_ms` to enforce a hard server-side timeout after which BigQuery automatically terminates the job.

The following code sample shows how to use `curl` to call the `execute_sql` MCP tool.

**Curl Request**

```
curl --location 'https://bigquery.googleapis.com/mcp' \
--header 'content-type: application/json' \
--header 'accept: application/json, text/event-stream' \
--data '{
  "method": "tools/call",
  "params": {
    "name": "execute_sql",
    "arguments": {
      // Provide these details according to the MCP tool specification.
    }
  },
  "jsonrpc": "2.0",
  "id": 1
}'
```

## Input Schema

Runs a BigQuery SQL query synchronously and returns query results if the query completes within a specified timeout.

### QueryRequest

**JSON representation**

```
{
  "projectId": string,
  "query": string,
  "dryRun": boolean,
  "labels": {
    string: string,
    ...
  },
  "jobTimeoutMs": string,
  "timeoutMs": integer
}
```

| Fields         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
|----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `projectId`    | `string` Required. Project that will be used for query execution and billing.                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| `query`        | `string` Required. The query to execute in the form of a GoogleSQL query.                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| `dryRun`       | `boolean` Optional. If set to true, BigQuery doesn't run the job. Instead, if the query is valid, BigQuery returns statistics about the job such as how many bytes would be processed. If the query is invalid, an error returns. The default value is false.                                                                                                                                                                                                                                                                            |
| `labels`       | `map (key: string, value: string)` Optional. The labels associated with this query. Labels can be used to organize and group query jobs. Label keys and values can be no longer than 63 characters, can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. Label keys must start with a letter and each label in the map must have a different key. An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` . |
| `jobTimeoutMs` | `string ( `[`Int64Value`](https://developers.google.com/discovery/v1/type-format)` format)` Optional. Optional: Job timeout in milliseconds. If this time limit is exceeded, BigQuery will attempt to stop the query job.                                                                                                                                                                                                                                                                                                                |
| `timeoutMs`    | `integer` Optional. Optional: Specifies the maximum amount of time, in milliseconds, that the client is willing to wait for the query to complete. By default, this limit is 20 seconds (20,000 milliseconds).                                                                                                                                                                                                                                                                                                                           |

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

### UInt32Value

**JSON representation**

```
{
  "value": integer
}
```

| Fields  |                                                                                                            |
|---------|------------------------------------------------------------------------------------------------------------|
| `value` | `integer ( `[`uint32`](https://developers.google.com/discovery/v1/type-format)` format)` The uint32 value. |

## Output Schema

Response for a BigQuery SQL query.

### QueryResponse

**JSON representation**

```
{
  "schema": {
    object (TableSchema)
  },
  "rows": [
    {
      object
    }
  ],
  "jobComplete": boolean,
  "errors": [
    {
      object (ErrorProto)
    }
  ],
  "queryId": string,
  "totalBytesBilled": string,
  "totalSlotMs": string,
  "numDmlAffectedRows": string,
  "totalBytesProcessed": string,
  "jobId": string
}
```

| Fields                |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
|-----------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `schema`              | `object ( `[`TableSchema`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.TableSchema)` )` The schema of the results. Present only when the query completes successfully.                                                                                                                                                                                                                                                                                                   |
| `rows[]`              | `object ( `[`Struct`](https://protobuf.dev/reference/protobuf/google.protobuf/#struct)` format)` An object with as many results as can be contained within the maximum permitted reply size. To get any additional rows, you can call GetQueryResults and specify the jobReference returned above.                                                                                                                                                                                                                             |
| `jobComplete`         | `boolean` Whether the query has completed or not. If rows or totalRows are present, this will always be true. If this is false, totalRows will not be available.                                                                                                                                                                                                                                                                                                                                                               |
| `errors[]`            | `object ( `[`ErrorProto`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.ErrorProto)` )` Output only. The first errors or warnings encountered during the running of the job. The final message includes the number of errors that caused the process to stop. Errors here do not necessarily mean that the job has completed or was unsuccessful. For more information about error messages, see [Error messages](https://cloud.google.com/bigquery/docs/error-messages) . |
| `queryId`             | `string` Output only. The ID of the query.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| `totalBytesBilled`    | `string ( `[`Int64Value`](https://developers.google.com/discovery/v1/type-format)` format)` Output only. The total number of bytes billed for the query. Only applies if the project is configured to use on-demand pricing.                                                                                                                                                                                                                                                                                                   |
| `totalSlotMs`         | `string ( `[`Int64Value`](https://developers.google.com/discovery/v1/type-format)` format)` Output only. Number of slot ms the user is actually billed for.                                                                                                                                                                                                                                                                                                                                                                    |
| `numDmlAffectedRows`  | `string ( `[`Int64Value`](https://developers.google.com/discovery/v1/type-format)` format)` Output only. The number of rows affected by a DML statement.                                                                                                                                                                                                                                                                                                                                                                       |
| `totalBytesProcessed` | `string ( `[`Int64Value`](https://developers.google.com/discovery/v1/type-format)` format)` Output only. The total number of bytes processed for this query.                                                                                                                                                                                                                                                                                                                                                                   |
| `jobId`               | `string` Output only. The ID of the BigQuery job created for this query, if any. Present when a query job is created (e.g. for long-running operations, DML, scripts). Use this ID with `get_query_results` , `cancel_job` , or `get_job` .                                                                                                                                                                                                                                                                                    |

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

### NullValue

Represents a JSON `null` .

`NullValue` is a sentinel, using an enum with only one value to represent the null value for the `Value` type union.

A field of type `NullValue` with any value other than `0` is considered invalid. Most ProtoJSON serializers will emit a `Value` with a `null_value` set as a JSON `null` regardless of the integer value, and so will round trip to a `0` value.

| Enums        |             |
|--------------|-------------|
| `NULL_VALUE` | Null value. |

### Tool Annotations

[Tool annotations](https://modelcontextprotocol.io/specification/latest/schema#toolannotations) are sent to MCP clients to describe the basic risk of a given tool. Most clients treat these hints as untrusted, but they can be used to decide when a confirmation prompt might be sent to a user.

Along with the title string, the following boolean hints are defined as follows:

- `readOnlyHint` : If true, the tool doesn't modify its environment. Default: false.
- `destructiveHint` : If true, then the tool can perform destructive actions. If false, then the tool can only perform additive actions. Default: true.
- `idempotentHint` : If true, then calling the tool repeatedly with the same arguments will have no additional effect on its environment. Default: false.
- `openWorldHint` : If true, then the tool can interact with an 'open world' of external entities. If false, then the tool can only interact with internal entities. For example, a web search tool would be open world, while a memory tool would not be open world.

Destructive Hint: ✅ \| Idempotent Hint: ❌ \| Read Only Hint: ❌ \| Open World Hint: ✅
