  - [Resource: DataPolicy](#DataPolicy)
      - [JSON representation](#DataPolicy.SCHEMA_REPRESENTATION)
  - [DataMaskingPolicy](#DataMaskingPolicy)
      - [JSON representation](#DataMaskingPolicy.SCHEMA_REPRESENTATION)
  - [PredefinedExpression](#PredefinedExpression)
  - [DataPolicyType](#DataPolicyType)
  - [Methods](#METHODS_SUMMARY)

## Resource: DataPolicy

Represents the label-policy binding.

<table>
<colgroup>
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
  &quot;dataPolicyType&quot;: enum (DataPolicyType),
  &quot;dataPolicyId&quot;: string,

  // Union field matching_label can be only one of the following:
  &quot;policyTag&quot;: string
  // End of list of possible types for union field matching_label.

  // Union field policy can be only one of the following:
  &quot;dataMaskingPolicy&quot;: {
    object (DataMaskingPolicy)
  }
  // End of list of possible types for union field policy.
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  name  `

`  string  `

Output only. Resource name of this data policy, in the format of `  projects/{projectNumber}/locations/{locationId}/dataPolicies/{dataPolicyId}  ` .

`  dataPolicyType  `

`  enum ( DataPolicyType  ` )

Required. Data policy type. Type of data policy.

`  dataPolicyId  `

`  string  `

User-assigned (human readable) ID of the data policy that needs to be unique within a project. Used as {dataPolicyId} in part of the resource name.

Union field `  matching_label  ` . Label that is bound to this data policy. `  matching_label  ` can be only one of the following:

`  policyTag  `

`  string  `

Policy tag resource name, in the format of `  projects/{projectNumber}/locations/{locationId}/taxonomies/{taxonomyId}/policyTags/{policyTag_id}  ` .

Union field `  policy  ` . The policy that is bound to this data policy. `  policy  ` can be only one of the following:

`  dataMaskingPolicy  `

`  object ( DataMaskingPolicy  ` )

The data masking policy that specifies the data masking rule to use.

## DataMaskingPolicy

The data masking policy that is used to specify data masking rule.

<table>
<colgroup>
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

  // Union field masking_expression can be only one of the following:
  &quot;predefinedExpression&quot;: enum (PredefinedExpression),
  &quot;routine&quot;: string
  // End of list of possible types for union field masking_expression.
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `  masking_expression  ` . A masking expression to bind to the data masking rule. `  masking_expression  ` can be only one of the following:

`  predefinedExpression  `

`  enum ( PredefinedExpression  ` )

A predefined masking expression.

`  routine  `

`  string  `

The name of the BigQuery routine that contains the custom masking routine, in the format of `  projects/{projectNumber}/datasets/{dataset_id}/routines/{routine_id}  ` .

## PredefinedExpression

The available masking rules. Learn more here: <https://cloud.google.com/bigquery/docs/column-data-masking-intro#masking_options> .

Enums

`  PREDEFINED_EXPRESSION_UNSPECIFIED  `

Default, unspecified predefined expression. No masking will take place since no expression is specified.

`  SHA256  `

Masking expression to replace data with SHA-256 hash.

`  ALWAYS_NULL  `

Masking expression to replace data with NULLs.

`  DEFAULT_MASKING_VALUE  `

Masking expression to replace data with their default masking values. The default masking values for each type listed as below:

  - STRING: ""
  - BYTES: b''
  - INTEGER: 0
  - FLOAT: 0.0
  - NUMERIC: 0
  - BOOLEAN: FALSE
  - TIMESTAMP: 1970-01-01 00:00:00 UTC
  - DATE: 1970-01-01
  - TIME: 00:00:00
  - DATETIME: 1970-01-01T00:00:00
  - GEOGRAPHY: POINT(0 0)
  - BIGNUMERIC: 0
  - ARRAY: \[\]
  - STRUCT: NOT\_APPLICABLE
  - JSON: NULL

`  LAST_FOUR_CHARACTERS  `

Masking expression shows the last four characters of text. The masking behavior is as follows:

  - If text length \> 4 characters: Replace text with XXXXX, append last four characters of original text.
  - If text length \<= 4 characters: Apply SHA-256 hash.

`  FIRST_FOUR_CHARACTERS  `

Masking expression shows the first four characters of text. The masking behavior is as follows:

  - If text length \> 4 characters: Replace text with XXXXX, prepend first four characters of original text.
  - If text length \<= 4 characters: Apply SHA-256 hash.

`  EMAIL_MASK  `

Masking expression for email addresses. The masking behavior is as follows:

  - Syntax-valid email address: Replace username with XXXXX. For example, <cloudysanfrancisco@gmail.com> becomes <XXXXX@gmail.com> .
  - Syntax-invalid email address: Apply SHA-256 hash.

For more information, see [Email mask](https://cloud.google.com/bigquery/docs/column-data-masking-intro#masking_options) .

`  DATE_YEAR_MASK  `

Masking expression to only show the *year* of `  Date  ` , `  DateTime  ` and `  TimeStamp  ` . For example, with the year 2076:

  - DATE : 2076-01-01
  - DATETIME : 2076-01-01T00:00:00
  - TIMESTAMP : 2076-01-01 00:00:00 UTC

Truncation occurs according to the UTC time zone. To change this, adjust the default time zone using the `  time_zone  ` system variable. For more information, see the [System variables reference](https://cloud.google.com/bigquery/docs/reference/system-variables) .

`  RANDOM_HASH  `

A masking expression that uses hashing to mask column data. It differs from SHA-256 in that a unique random value is generated for each query and is added to the hash input, resulting in a different masked result for each query. Creating and updating a data policy with a `  RANDOM_HASH  ` masking expression is only supported for the Data Policy v2 API.

## DataPolicyType

A list of supported data policy types.

Enums

`  DATA_POLICY_TYPE_UNSPECIFIED  `

Default value for the data policy type. This should not be used.

`  COLUMN_LEVEL_SECURITY_POLICY  `

Used to create a data policy for column-level security, without data masking.

`  DATA_MASKING_POLICY  `

Used to create a data policy for data masking.

## Methods

### `             create           `

Creates a new data policy under a project with the given `  dataPolicyId  ` (used as the display name), policy tag, and data policy type.

### `             delete           `

Deletes the data policy specified by its resource name.

### `             get           `

Gets the data policy specified by its resource name.

### `             getIamPolicy           `

Gets the IAM policy for the specified data policy.

### `             list           `

List all of the data policies in the specified parent project.

### `             patch           `

Updates the metadata for an existing data policy.

### `             rename           `

Renames the id (display name) of the specified data policy.

### `             setIamPolicy           `

Sets the IAM policy for the specified data policy.

### `             testIamPermissions           `

Returns the caller's permission on the specified data policy resource.
