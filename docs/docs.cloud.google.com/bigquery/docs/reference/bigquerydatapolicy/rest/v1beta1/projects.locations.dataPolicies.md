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

**JSON representation**

```
{
  "name": string,
  "dataPolicyType": enum (DataPolicyType),
  "dataPolicyId": string,

  // The following is a list of mutually exclusive fields. At most one of the
  // fields will be set in a response:
  "policyTag": string
  // End of mutually exclusive fields.

  // The following is a list of mutually exclusive fields. At most one of the
  // fields will be set in a response:
  "dataMaskingPolicy": {
    object (DataMaskingPolicy)
  }
  // End of mutually exclusive fields.
}
```

| Fields                                                                                                                                                   |                                                                                                                                                                                                                                                    |
|----------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`                                                                                                                                                   | `string` Output only. Resource name of this data policy, in the format of `projects/{projectNumber}/locations/{locationId}/dataPolicies/{dataPolicyId}` .                                                                                          |
| `dataPolicyType`                                                                                                                                         | `enum ( `[`DataPolicyType`](https://docs.cloud.google.com/bigquery/docs/reference/bigquerydatapolicy/rest/v1beta1/projects.locations.dataPolicies#DataPolicyType)` )` Required. Data policy type. Type of data policy.                             |
| `dataPolicyId`                                                                                                                                           | `string` User-assigned (human readable) ID of the data policy that needs to be unique within a project. Used as {dataPolicyId} in part of the resource name.                                                                                       |
| Label that is bound to this data policy. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:      |                                                                                                                                                                                                                                                    |
| `policyTag`                                                                                                                                              | `string` Policy tag resource name, in the format of `projects/{projectNumber}/locations/{locationId}/taxonomies/{taxonomyId}/policyTags/{policyTag_id}` .                                                                                          |
| End of mutually exclusive fields.                                                                                                                        |                                                                                                                                                                                                                                                    |
| The policy that is bound to this data policy. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response: |                                                                                                                                                                                                                                                    |
| `dataMaskingPolicy`                                                                                                                                      | `object ( `[`DataMaskingPolicy`](https://docs.cloud.google.com/bigquery/docs/reference/bigquerydatapolicy/rest/v1beta1/projects.locations.dataPolicies#DataMaskingPolicy)` )` The data masking policy that specifies the data masking rule to use. |
| End of mutually exclusive fields.                                                                                                                        |                                                                                                                                                                                                                                                    |

## DataMaskingPolicy

The data masking policy that is used to specify data masking rule.

**JSON representation**

```
{

  // The following is a list of mutually exclusive fields. At most one of the
  // fields will be set in a response:
  "predefinedExpression": enum (PredefinedExpression)
  // End of mutually exclusive fields.
}
```

| Fields                                                                                                                                                            |                                                                                                                                                                                                                    |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| A masking expression to bind to the data masking rule. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response: |                                                                                                                                                                                                                    |
| `predefinedExpression`                                                                                                                                            | `enum ( `[`PredefinedExpression`](https://docs.cloud.google.com/bigquery/docs/reference/bigquerydatapolicy/rest/v1beta1/projects.locations.dataPolicies#PredefinedExpression)` )` A predefined masking expression. |
| End of mutually exclusive fields.                                                                                                                                 |                                                                                                                                                                                                                    |

## PredefinedExpression

The available masking rules. Learn more here: <https://cloud.google.com/bigquery/docs/column-data-masking-intro#masking_options> .

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Enums</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>PREDEFINED_EXPRESSION_UNSPECIFIED</code></td>
<td>Default, unspecified predefined expression. No masking will take place since no expression is specified.</td>
</tr>
<tr class="even">
<td><code>SHA256</code></td>
<td>Masking expression to replace data with SHA-256 hash.</td>
</tr>
<tr class="odd">
<td><code>ALWAYS_NULL</code></td>
<td>Masking expression to replace data with NULLs.</td>
</tr>
<tr class="even">
<td><code>DEFAULT_MASKING_VALUE</code></td>
<td><p>Masking expression to replace data with their default masking values. The default masking values for each type listed as below:</p>
<ul>
<li>STRING: ""</li>
<li>BYTES: b''</li>
<li>INTEGER: 0</li>
<li>FLOAT: 0.0</li>
<li>NUMERIC: 0</li>
<li>BOOLEAN: FALSE</li>
<li>TIMESTAMP: 1970-01-01 00:00:00 UTC</li>
<li>DATE: 1970-01-01</li>
<li>TIME: 00:00:00</li>
<li>DATETIME: 1970-01-01T00:00:00</li>
<li>GEOGRAPHY: POINT(0 0)</li>
<li>BIGNUMERIC: 0</li>
<li>ARRAY: []</li>
<li>STRUCT: NOT_APPLICABLE</li>
<li>JSON: NULL</li>
</ul></td>
</tr>
</tbody>
</table>

## DataPolicyType

A list of supported data policy types.

| Enums                          |                                                                               |
|--------------------------------|-------------------------------------------------------------------------------|
| `DATA_POLICY_TYPE_UNSPECIFIED` | Default value for the data policy type. This should not be used.              |
| `COLUMN_LEVEL_SECURITY_POLICY` | Used to create a data policy for column-level security, without data masking. |
| `DATA_MASKING_POLICY`          | Used to create a data policy for data masking.                                |

| Methods                                                                                                                                                          |                                                                                                                                       |
|------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| [`create`](https://docs.cloud.google.com/bigquery/docs/reference/bigquerydatapolicy/rest/v1beta1/projects.locations.dataPolicies/create)                         | Creates a new data policy under a project with the given `dataPolicyId` (used as the display name), policy tag, and data policy type. |
| [`delete`](https://docs.cloud.google.com/bigquery/docs/reference/bigquerydatapolicy/rest/v1beta1/projects.locations.dataPolicies/delete)                         | Deletes the data policy specified by its resource name.                                                                               |
| [`get`](https://docs.cloud.google.com/bigquery/docs/reference/bigquerydatapolicy/rest/v1beta1/projects.locations.dataPolicies/get)                               | Gets the data policy specified by its resource name.                                                                                  |
| [`getIamPolicy`](https://docs.cloud.google.com/bigquery/docs/reference/bigquerydatapolicy/rest/v1beta1/projects.locations.dataPolicies/getIamPolicy)             | Gets the IAM policy for the specified data policy.                                                                                    |
| [`list`](https://docs.cloud.google.com/bigquery/docs/reference/bigquerydatapolicy/rest/v1beta1/projects.locations.dataPolicies/list)                             | List all of the data policies in the specified parent project.                                                                        |
| [`patch`](https://docs.cloud.google.com/bigquery/docs/reference/bigquerydatapolicy/rest/v1beta1/projects.locations.dataPolicies/patch)                           | Updates the metadata for an existing data policy.                                                                                     |
| [`setIamPolicy`](https://docs.cloud.google.com/bigquery/docs/reference/bigquerydatapolicy/rest/v1beta1/projects.locations.dataPolicies/setIamPolicy)             | Sets the IAM policy for the specified data policy.                                                                                    |
| [`testIamPermissions`](https://docs.cloud.google.com/bigquery/docs/reference/bigquerydatapolicy/rest/v1beta1/projects.locations.dataPolicies/testIamPermissions) | Returns the caller's permission on the specified data policy resource.                                                                |
