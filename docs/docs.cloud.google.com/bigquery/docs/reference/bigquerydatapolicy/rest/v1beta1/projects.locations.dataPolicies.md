---
name: documents/docs.cloud.google.com/bigquery/docs/reference/bigquerydatapolicy/rest/v1beta1/projects.locations.dataPolicies
uri: https://docs.cloud.google.com/bigquery/docs/reference/bigquerydatapolicy/rest/v1beta1/projects.locations.dataPolicies
title: 'REST Resource: projects.locations.dataPolicies'
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

  - [Resource: DataPolicy](https://docs.cloud.google.com/bigquery/docs/reference/bigquerydatapolicy/rest/v1beta1/projects.locations.dataPolicies#DataPolicy)
      - [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/bigquerydatapolicy/rest/v1beta1/projects.locations.dataPolicies#DataPolicy.SCHEMA_REPRESENTATION)
  - [DataMaskingPolicy](https://docs.cloud.google.com/bigquery/docs/reference/bigquerydatapolicy/rest/v1beta1/projects.locations.dataPolicies#DataMaskingPolicy)
      - [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/bigquerydatapolicy/rest/v1beta1/projects.locations.dataPolicies#DataMaskingPolicy.SCHEMA_REPRESENTATION)
  - [PredefinedExpression](https://docs.cloud.google.com/bigquery/docs/reference/bigquerydatapolicy/rest/v1beta1/projects.locations.dataPolicies#PredefinedExpression)
  - [DataPolicyType](https://docs.cloud.google.com/bigquery/docs/reference/bigquerydatapolicy/rest/v1beta1/projects.locations.dataPolicies#DataPolicyType)
  - [Methods](https://docs.cloud.google.com/bigquery/docs/reference/bigquerydatapolicy/rest/v1beta1/projects.locations.dataPolicies#METHODS_SUMMARY)

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;dataPolicyType&quot;: enum (DataPolicyType),&quot;dataPolicyId&quot;: string,// The following is a list of mutually exclusive fields. At most one of the// fields will be set in a response:&quot;policyTag&quot;: string// End of mutually exclusive fields.// The following is a list of mutually exclusive fields. At most one of the// fields will be set in a response:&quot;dataMaskingPolicy&quot;: {object (DataMaskingPolicy)}// End of mutually exclusive fields.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`name`

`string`

Output only. Resource name of this data policy, in the format of `projects/{projectNumber}/locations/{locationId}/dataPolicies/{dataPolicyId}` .

`dataPolicyType`

` enum ( DataPolicyType  ` )

Required. Data policy type. Type of data policy.

`dataPolicyId`

`string`

User-assigned (human readable) ID of the data policy that needs to be unique within a project. Used as {dataPolicyId} in part of the resource name.

Label that is bound to this data policy. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`policyTag`

`string`

Policy tag resource name, in the format of `projects/{projectNumber}/locations/{locationId}/taxonomies/{taxonomyId}/policyTags/{policyTag_id}` .

End of mutually exclusive fields.

The policy that is bound to this data policy. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`dataMaskingPolicy`

` object ( DataMaskingPolicy  ` )

The data masking policy that specifies the data masking rule to use.

End of mutually exclusive fields.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// The following is a list of mutually exclusive fields. At most one of the// fields will be set in a response:&quot;predefinedExpression&quot;: enum (PredefinedExpression)// End of mutually exclusive fields.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

A masking expression to bind to the data masking rule. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`predefinedExpression`

` enum ( PredefinedExpression  ` )

A predefined masking expression.

End of mutually exclusive fields.

## PredefinedExpression

The available masking rules. Learn more here: <https://cloud.google.com/bigquery/docs/column-data-masking-intro#masking_options> .

Enums

`PREDEFINED_EXPRESSION_UNSPECIFIED`

Default, unspecified predefined expression. No masking will take place since no expression is specified.

`SHA256`

Masking expression to replace data with SHA-256 hash.

`ALWAYS_NULL`

Masking expression to replace data with NULLs.

`DEFAULT_MASKING_VALUE`

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

`DATA_POLICY_TYPE_UNSPECIFIED`

Default value for the data policy type. This should not be used.

`COLUMN_LEVEL_SECURITY_POLICY`

Used to create a data policy for column-level security, without data masking.

`DATA_MASKING_POLICY`

Used to create a data policy for data masking.

## Methods

### `            create           `

Creates a new data policy under a project with the given `dataPolicyId` (used as the display name), policy tag, and data policy type.

### `            delete           `

Deletes the data policy specified by its resource name.

### `            get           `

Gets the data policy specified by its resource name.

### `            getIamPolicy           `

Gets the IAM policy for the specified data policy.

### `            list           `

List all of the data policies in the specified parent project.

### `            patch           `

Updates the metadata for an existing data policy.

### `            setIamPolicy           `

Sets the IAM policy for the specified data policy.

### `            testIamPermissions           `

Returns the caller's permission on the specified data policy resource.
