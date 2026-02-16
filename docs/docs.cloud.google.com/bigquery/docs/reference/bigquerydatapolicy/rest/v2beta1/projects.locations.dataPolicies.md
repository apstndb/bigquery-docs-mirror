  - [Resource: DataPolicy](#DataPolicy)
      - [JSON representation](#DataPolicy.SCHEMA_REPRESENTATION)
  - [DataMaskingPolicy](#DataMaskingPolicy)
      - [JSON representation](#DataMaskingPolicy.SCHEMA_REPRESENTATION)
  - [PredefinedExpression](#PredefinedExpression)
  - [DataPolicyType](#DataPolicyType)
  - [Version](#Version)
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
  &quot;dataPolicyId&quot;: string,
  &quot;dataPolicyType&quot;: enum (DataPolicyType),
  &quot;policyTag&quot;: string,
  &quot;grantees&quot;: [
    string
  ],
  &quot;version&quot;: enum (Version),

  // Union field policy can be only one of the following:
  &quot;dataMaskingPolicy&quot;: {
    object (DataMaskingPolicy)
  }
  // End of list of possible types for union field policy.
  &quot;etag&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  name  `

`  string  `

Identifier. Resource name of this data policy, in the format of `  projects/{projectNumber}/locations/{locationId}/dataPolicies/{dataPolicyId}  ` .

`  dataPolicyId  `

`  string  `

Output only. User-assigned (human readable) ID of the data policy that needs to be unique within a project. Used as {dataPolicyId} in part of the resource name.

`  dataPolicyType  `

`  enum ( DataPolicyType  ` )

Required. Type of data policy.

`  policyTag  `

`  string  `

Output only. Policy tag resource name, in the format of `  projects/{projectNumber}/locations/{locationId}/taxonomies/{taxonomyId}/policyTags/{policyTag_id}  ` . policyTag is supported only for V1 data policies.

`  grantees[]  `

`  string  `

Optional. The list of IAM principals that have Fine Grained Access to the underlying data goverened by this data policy.

Uses the [IAM V2 principal syntax](https://cloud.google.com/iam/docs/principal-identifiers#v2) Only supports principal types users, groups, serviceaccounts, cloudidentity. This field is supported in V2 Data Policy only. In case of V1 data policies (i.e. verion = 1 and policyTag is set), this field is not populated.

`  version  `

`  enum ( Version  ` )

Output only. The version of the Data Policy resource.

Union field `  policy  ` . The policy that is bound to this data policy. `  policy  ` can be only one of the following:

`  dataMaskingPolicy  `

`  object ( DataMaskingPolicy  ` )

Optional. The data masking policy that specifies the data masking rule to use. It must be set if the data policy type is DATA\_MASKING\_POLICY.

`  etag  `

`  string  `

The etag for this Data Policy. This field is used for dataPolicies.patch calls. If Data Policy exists, this field is required and must match the server's etag. It will also be populated in the response of dataPolicies.get, dataPolicies.create, and dataPolicies.patch calls.

## DataMaskingPolicy

The policy used to specify data masking rule.

<table>
<colgroup>
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
  &quot;predefinedExpression&quot;: enum (PredefinedExpression)
  // End of list of possible types for union field masking_expression.
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `  masking_expression  ` . A masking expression to bind to the data masking rule. `  masking_expression  ` can be only one of the following:

`  predefinedExpression  `

`  enum ( PredefinedExpression  ` )

Optional. A predefined masking expression.

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

## DataPolicyType

A list of supported data policy types.

Enums

`  DATA_POLICY_TYPE_UNSPECIFIED  `

Default value for the data policy type. This should not be used.

`  DATA_MASKING_POLICY  `

Used to create a data policy for data masking.

`  RAW_DATA_ACCESS_POLICY  `

Used to create a data policy for raw data access.

`  COLUMN_LEVEL_SECURITY_POLICY  `

Used to create a data policy for column-level security, without data masking. This is deprecated in V2 api and only present to support GET and LIST operations for V1 data policies in V2 api.

## Version

The supported versions for the Data Policy resource.

Enums

`  VERSION_UNSPECIFIED  `

Default value for the data policy version. This should not be used.

`  V1  `

V1 data policy version. V1 Data Policies will be present in V2 List api response, but can not be created/updated/deleted from V2 api.

`  V2  `

V2 data policy version.

## Methods

### `             addGrantees           `

Adds new grantees to a data policy.

### `             create           `

Creates a new data policy under a project with the given `  data_policy_id  ` (used as the display name), and data policy type.

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

### `             removeGrantees           `

Removes grantees from a data policy.

### `             setIamPolicy           `

Sets the IAM policy for the specified data policy.

### `             testIamPermissions           `

Returns the caller's permission on the specified data policy resource.
