---
name: documents/docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/execute_sql_readonly
uri: https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/execute_sql_readonly
title: 'MCP Tools Reference: bigquery.googleapis.com'
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

## Tool: `execute_sql_readonly`

Run a read-only SQL query in the project and return the result. Prefer this tool over `execute_sql` if possible.

This tool is restricted to only `SELECT` statements. `INSERT` , `UPDATE` , and `DELETE` statements and stored procedures aren't allowed. If the query doesn't include a `SELECT` statement, an error is returned. For information on creating queries, see the [GoogleSQL documentation](https://cloud.google.com/bigquery/docs/reference/standard-sql/query-syntax) .

Example Queries:

```sql
-- Count the number of penguins in each island.
        SELECT island, COUNT(*) AS population
        FROM bigquery-public-data.ml_datasets.penguins GROUP BY island

        -- Evaluate a bigquery ML Model.
        SELECT * FROM ML.EVALUATE(MODEL `my_dataset.my_model`)

        -- Evaluate BigQuery ML model on custom data
        SELECT *
        FROM ML.EVALUATE(MODEL `my_dataset.my_model`, (SELECT * FROM `my_dataset.my_table`))

        -- Predict using BigQuery ML model:
        SELECT *
        FROM ML.PREDICT(MODEL `my_dataset.my_model`, (SELECT * FROM `my_dataset.my_table`))

        -- Forecast data using AI.FORECAST
        SELECT *
        FROM AI.FORECAST(TABLE `project.dataset.my_table`, data_col => 'num_trips',
          timestamp_col => 'date', id_cols => ['usertype'], horizon => 30)
        
```

Queries executed using the `execute_sql_readonly` tool will always have the job label `goog-mcp-server: true` automatically set in addition to any custom `labels` provided in the request. Queries are charged to the project specified in the `project_id` field.

The following code sample shows how to use `curl` to call the `execute_sql_readonly` MCP tool.

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
    &quot;name&quot;: &quot;execute_sql_readonly&quot;,
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

Runs a BigQuery SQL query synchronously and returns query results if the query completes within a specified timeout.

### QueryRequest

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
  &quot;query&quot;: string,
  &quot;dryRun&quot;: boolean,
  &quot;labels&quot;: {
    string: string,
    ...
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`projectId`

`string`

Required. Project that will be used for query execution and billing.

`query`

`string`

Required. The query to execute in the form of a GoogleSQL query.

`dryRun`

`boolean`

Optional. If set to true, BigQuery doesn't run the job. Instead, if the query is valid, BigQuery returns statistics about the job such as how many bytes would be processed. If the query is invalid, an error returns. The default value is false.

`labels`

`map (key: string, value: string)`

Optional. The labels associated with this query. Labels can be used to organize and group query jobs. Label keys and values can be no longer than 63 characters, can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. Label keys must start with a letter and each label in the map must have a different key.

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

## Output Schema

Response for a BigQuery SQL query.

### QueryResponse

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;schema&quot;: {object (TableSchema)},&quot;rows&quot;: [{object}],&quot;jobComplete&quot;: boolean,&quot;errors&quot;: [{object (ErrorProto)}],&quot;queryId&quot;: string,&quot;totalBytesBilled&quot;: string,&quot;totalSlotMs&quot;: string,&quot;numDmlAffectedRows&quot;: string,&quot;totalBytesProcessed&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`schema`

` object ( TableSchema  ` )

The schema of the results. Present only when the query completes successfully.

`rows[]`

` object ( Struct  ` format)

An object with as many results as can be contained within the maximum permitted reply size. To get any additional rows, you can call GetQueryResults and specify the jobReference returned above.

`jobComplete`

`boolean`

Whether the query has completed or not. If rows or totalRows are present, this will always be true. If this is false, totalRows will not be available.

`errors[]`

` object ( ErrorProto  ` )

Output only. The first errors or warnings encountered during the running of the job. The final message includes the number of errors that caused the process to stop. Errors here do not necessarily mean that the job has completed or was unsuccessful. For more information about error messages, see [Error messages](https://cloud.google.com/bigquery/docs/error-messages) .

`queryId`

`string`

Output only. The ID of the query.

`totalBytesBilled`

`string ( Int64Value format)`

Output only. The total number of bytes billed for the query. Only applies if the project is configured to use on-demand pricing.

`totalSlotMs`

`string ( Int64Value format)`

Output only. Number of slot ms the user is actually billed for.

`numDmlAffectedRows`

`string ( Int64Value format)`

Output only. The number of rows affected by a DML statement.

`totalBytesProcessed`

`string ( Int64Value format)`

Output only. The total number of bytes processed for this query.

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

### NullValue

Represents a JSON `null` .

`NullValue` is a sentinel, using an enum with only one value to represent the null value for the `Value` type union.

A field of type `NullValue` with any value other than `0` is considered invalid. Most ProtoJSON serializers will emit a `Value` with a `null_value` set as a JSON `null` regardless of the integer value, and so will round trip to a `0` value.

Enums

`NULL_VALUE`

Null value.

### Tool Annotations

[Tool annotations](https://modelcontextprotocol.io/specification/latest/schema#toolannotations) are sent to MCP clients to describe the basic risk of a given tool. Most clients treat these hints as untrusted, but they can be used to decide when a confirmation prompt might be sent to a user.

Along with the title string, the following boolean hints are defined as follows:

  - `readOnlyHint` : If true, the tool doesn't modify its environment. Default: false.
  - `destructiveHint` : If true, then the tool can perform destructive actions. If false, then the tool can only perform additive actions. Default: true.
  - `idempotentHint` : If true, then calling the tool repeatedly with the same arguments will have no additional effect on its environment. Default: false.
  - `openWorldHint` : If true, then the tool can interact with an 'open world' of external entities. If false, then the tool can only interact with internal entities. For example, a web search tool would be open world, while a memory tool would not be open world.

Destructive Hint: ❌ | Idempotent Hint: ✅ | Read Only Hint: ✅ | Open World Hint: ❌
