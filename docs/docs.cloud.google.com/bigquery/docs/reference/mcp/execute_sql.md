## Tool: `       execute_sql      `

Run a SQL query in the project and return the result.

This tool is restricted to only `  SELECT  ` statements. `  INSERT  ` , `  UPDATE  ` , and `  DELETE  ` statements and stored procedures aren't allowed. If the query doesn't include a `  SELECT  ` statement, an error is returned. For information on creating queries, see the [GoogleSQL documentation](https://cloud.google.com/bigquery/docs/reference/standard-sql/query-syntax) .

The `  execute_sql  ` tool can also have side effects if the the query invokes [remote functions](https://cloud.google.com/bigquery/docs/remote-functions) or [Python UDFs](https://cloud.google.com/bigquery/docs/user-defined-functions-python) .

All queries that are run using the `  execute_sql  ` tool have a label that identifies the tool as the source. You can use this label to filter the queries using the label and value pair `  goog-mcp-server: true  ` .

Queries are charged to the project specified in the `  project_id  ` field.

The following sample demonstrate how to use `  curl  ` to invoke the `  execute_sql  ` MCP tool.

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
<td><pre class="text" dir="ltr" data-is-upgraded="" data-syntax="Bash" translate="no"><code>                  
curl --location &#39;https://bigquery.googleapis.com/mcp&#39; \
--header &#39;content-type: application/json&#39; \
--header &#39;accept: application/json, text/event-stream&#39; \
--data &#39;{
  &quot;method&quot;: &quot;tools/call&quot;,
  &quot;params&quot;: {
    &quot;name&quot;: &quot;execute_sql&quot;,
    &quot;arguments&quot;: {
      // provide these details according to the tool&#39;s MCP specification
    }
  },
  &quot;jsonrpc&quot;: &quot;2.0&quot;,
  &quot;id&quot;: 1
}&#39;
                </code></pre></td>
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
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;projectId&quot;: string,
  &quot;query&quot;: string,
  &quot;dryRun&quot;: boolean
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  projectId  `

`  string  `

Required. Project that will be used for query execution and billing.

`  query  `

`  string  `

Required. The query to execute in the form of a GoogleSQL query.

`  dryRun  `

`  boolean  `

Optional. If set to true, BigQuery doesn't run the job. Instead, if the query is valid, BigQuery returns statistics about the job such as how many bytes would be processed. If the query is invalid, an error returns. The default value is false.

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
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;schema&quot;: {
    object (TableSchema)
  },
  &quot;rows&quot;: [
    {
      object
    }
  ],
  &quot;jobComplete&quot;: boolean,
  &quot;errors&quot;: [
    {
      object (ErrorProto)
    }
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  schema  `

`  object ( TableSchema  ` )

The schema of the results. Present only when the query completes successfully.

`  rows[]  `

`  object ( Struct  ` format)

An object with as many results as can be contained within the maximum permitted reply size. To get any additional rows, you can call GetQueryResults and specify the jobReference returned above.

`  jobComplete  `

`  boolean  `

Whether the query has completed or not. If rows or totalRows are present, this will always be true. If this is false, totalRows will not be available.

`  errors[]  `

`  object ( ErrorProto  ` )

Output only. The first errors or warnings encountered during the running of the job. The final message includes the number of errors that caused the process to stop. Errors here do not necessarily mean that the job has completed or was unsuccessful. For more information about error messages, see [Error messages](https://cloud.google.com/bigquery/docs/error-messages) .

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
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;fields&quot;: [
    {
      object (TableFieldSchema)
    }
  ],
  &quot;foreignTypeInfo&quot;: {
    object (ForeignTypeInfo)
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  fields[]  `

`  object ( TableFieldSchema  ` )

Describes the fields in a table.

`  foreignTypeInfo  `

`  object ( ForeignTypeInfo  ` )

Optional. Specifies metadata of the foreign data type definition in field schema ( `  TableFieldSchema.foreign_type_definition  ` ).

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
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;name&quot;: string,
  &quot;type&quot;: string,
  &quot;mode&quot;: string,
  &quot;fields&quot;: [
    {
      object (TableFieldSchema)
    }
  ],
  &quot;description&quot;: string,
  &quot;policyTags&quot;: {
    object (PolicyTagList)
  },
  &quot;dataPolicies&quot;: [
    {
      object (DataPolicyOption)
    }
  ],
  &quot;maxLength&quot;: string,
  &quot;precision&quot;: string,
  &quot;scale&quot;: string,
  &quot;timestampPrecision&quot;: string,
  &quot;roundingMode&quot;: enum (RoundingMode),
  &quot;collation&quot;: string,
  &quot;defaultValueExpression&quot;: string,
  &quot;rangeElementType&quot;: {
    object (FieldElementType)
  },
  &quot;foreignTypeDefinition&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  name  `

`  string  `

Required. The field name. The name must contain only letters (a-z, A-Z), numbers (0-9), or underscores (\_), and must start with a letter or underscore. The maximum length is 300 characters.

`  type  `

`  string  `

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

`  mode  `

`  string  `

Optional. The field mode. Possible values include NULLABLE, REQUIRED and REPEATED. The default value is NULLABLE.

`  fields[]  `

`  object ( TableFieldSchema  ` )

Optional. Describes the nested schema fields if the type property is set to RECORD.

`  description  `

`  string  `

Optional. The field description. The maximum length is 1,024 characters.

`  policyTags  `

`  object ( PolicyTagList  ` )

Optional. The policy tags attached to this field, used for field-level access control. If not set, defaults to empty policy\_tags.

`  dataPolicies[]  `

`  object ( DataPolicyOption  ` )

Optional. Data policies attached to this field, used for field-level access control.

`  maxLength  `

`  string ( int64 format)  `

Optional. Maximum length of values of this field for STRINGS or BYTES.

If max\_length is not specified, no maximum length constraint is imposed on this field.

If type = "STRING", then max\_length represents the maximum UTF-8 length of strings in this field.

If type = "BYTES", then max\_length represents the maximum number of bytes in this field.

It is invalid to set this field if type ≠ "STRING" and ≠ "BYTES".

`  precision  `

`  string ( int64 format)  `

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

`  scale  `

`  string ( int64 format)  `

Optional. See documentation for precision.

`  timestampPrecision  `

`  string ( Int64Value format)  `

Optional. Precision (maximum number of total digits in base 10) for seconds of TIMESTAMP type.

Possible values include: \* 6 (Default, for TIMESTAMP type with microsecond precision) \* 12 (For TIMESTAMP type with picosecond precision)

`  roundingMode  `

`  enum ( RoundingMode  ` )

Optional. Specifies the rounding mode to be used when storing values of NUMERIC and BIGNUMERIC type.

`  collation  `

`  string  `

Optional. Field collation can be set only when the type of field is STRING. The following values are supported:

  - 'und:ci': undetermined locale, case insensitive.
  - '': empty string. Default to case-sensitive behavior.

`  defaultValueExpression  `

`  string  `

Optional. A SQL expression to specify the [default value](https://cloud.google.com/bigquery/docs/default-values) for this field.

`  rangeElementType  `

`  object ( FieldElementType  ` )

Optional. The subtype of the RANGE, if the type of this field is RANGE. If the type is RANGE, this field is required. Values for the field element type can be the following:

  - DATE
  - DATETIME
  - TIMESTAMP

`  foreignTypeDefinition  `

`  string  `

Optional. Definition of the foreign data type. Only valid for top-level schema fields (not nested fields). If the type is FOREIGN, this field is required.

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
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;value&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  value  `

`  string  `

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
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;names&quot;: [
    string
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  names[]  `

`  string  `

A list of policy tag resource names. For example, "projects/1/locations/eu/taxonomies/2/policyTags/3". At most 1 policy tag is currently allowed.

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
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{

  // Union field _name can be only one of the following:
  &quot;name&quot;: string
  // End of list of possible types for union field _name.
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `  _name  ` .

`  _name  ` can be only one of the following:

`  name  `

`  string  `

Data policy resource name in the form of projects/project\_id/locations/location\_id/dataPolicies/data\_policy\_id.

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
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;value&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  value  `

`  string ( int64 format)  `

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
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;type&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  type  `

`  string  `

Required. The type of a field element. For more information, see `  TableFieldSchema.type  ` .

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
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;typeSystem&quot;: enum (TypeSystem)
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  typeSystem  `

`  enum ( TypeSystem  ` )

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
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;fields&quot;: {
    string: value,
    ...
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  fields  `

`  map (key: string, value: value ( Value  ` format))

Unordered map of dynamically typed values.

An object containing a list of `  "key": value  ` pairs. Example: `  { "name": "wrench", "mass": "1.3kg", "count": "3" }  ` .

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
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;key&quot;: string,
  &quot;value&quot;: value
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  key  `

`  string  `

`  value  `

`  value ( Value  ` format)

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
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{

  // Union field kind can be only one of the following:
  &quot;nullValue&quot;: null,
  &quot;numberValue&quot;: number,
  &quot;stringValue&quot;: string,
  &quot;boolValue&quot;: boolean,
  &quot;structValue&quot;: {
    object
  },
  &quot;listValue&quot;: array
  // End of list of possible types for union field kind.
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `  kind  ` . The kind of value. `  kind  ` can be only one of the following:

`  nullValue  `

`  null  `

Represents a null value.

`  numberValue  `

`  number  `

Represents a double value.

`  stringValue  `

`  string  `

Represents a string value.

`  boolValue  `

`  boolean  `

Represents a boolean value.

`  structValue  `

`  object ( Struct  ` format)

Represents a structured value.

`  listValue  `

`  array ( ListValue  ` format)

Represents a repeated `  Value  ` .

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
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;values&quot;: [
    value
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  values[]  `

`  value ( Value  ` format)

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
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;value&quot;: boolean
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  value  `

`  boolean  `

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
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;reason&quot;: string,
  &quot;location&quot;: string,
  &quot;debugInfo&quot;: string,
  &quot;message&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  reason  `

`  string  `

A short error code that summarizes the error.

`  location  `

`  string  `

Specifies where the error occurred, if present.

`  debugInfo  `

`  string  `

Debugging information. This property is internal to Google and should not be used.

`  message  `

`  string  `

A human-readable description of the error.

### Tool Annotations

Destructive Hint: ✅ | Idempotent Hint: ❌ | Read Only Hint: ❌ | Open World Hint: ✅
