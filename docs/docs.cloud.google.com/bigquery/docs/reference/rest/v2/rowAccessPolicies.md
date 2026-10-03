---
name: documents/docs.cloud.google.com/bigquery/docs/reference/rest/v2/rowAccessPolicies
uri: https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/rowAccessPolicies
title: 'REST Resource: rowAccessPolicies'
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

- [Resource: RowAccessPolicy](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/rowAccessPolicies#RowAccessPolicy)
  - [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/rowAccessPolicies#RowAccessPolicy.SCHEMA_REPRESENTATION)
- [RowAccessPolicyReference](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/rowAccessPolicies#RowAccessPolicyReference)
  - [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/rowAccessPolicies#RowAccessPolicyReference.SCHEMA_REPRESENTATION)
- [Methods](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/rowAccessPolicies#METHODS_SUMMARY)

## Resource: RowAccessPolicy

Represents access on a subset of rows on the specified table, defined by its filter predicate. Access to the subset of rows is controlled by its IAM policy.

**JSON representation**

```
{
  "etag": string,
  "rowAccessPolicyReference": {
    object (RowAccessPolicyReference)
  },
  "filterPredicate": string,
  "creationTime": string,
  "lastModifiedTime": string,
  "grantees": [
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
<td><code>etag</code></td>
<td><p><code>string</code></p>
<p>Output only. A hash of this resource.</p></td>
</tr>
<tr class="even">
<td><code>rowAccessPolicyReference</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/rowAccessPolicies#RowAccessPolicyReference"><code>RowAccessPolicyReference</code></a><code> )</code></p>
<p>Required. Reference describing the ID of this row access policy.</p></td>
</tr>
<tr class="odd">
<td><code>filterPredicate</code></td>
<td><p><code>string</code></p>
<p>Required. A SQL boolean expression that represents the rows defined by this row access policy, similar to the boolean expression in a WHERE clause of a SELECT query on a table. References to other tables, routines, and temporary functions are not supported.</p>
<p>Examples: region="EU" date_field = CAST('2019-9-27' as DATE) nullable_field is not NULL numeric_field BETWEEN 1.0 AND 5.0</p></td>
</tr>
<tr class="even">
<td><code>creationTime</code></td>
<td><p><code>string ( </code><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp"><code>Timestamp</code></a><code> format)</code></p>
<p>Output only. The time when this row access policy was created, in milliseconds since the epoch.</p></td>
</tr>
<tr class="odd">
<td><code>lastModifiedTime</code></td>
<td><p><code>string ( </code><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp"><code>Timestamp</code></a><code> format)</code></p>
<p>Output only. The time when this row access policy was last modified, in milliseconds since the epoch.</p></td>
</tr>
<tr class="even">
<td><code>grantees[]</code></td>
<td><p><code>string</code></p>
<p>Optional. Input only. The optional list of iamMember users or groups that specifies the initial members that the row-level access policy should be created with.</p>
<p>grantees types:</p>
<ul>
<li>"user: <a href="mailto:alice@example.com%22">alice@example.com"</a> : An email address that represents a specific Google account.</li>
<li>"serviceAccount: <a href="mailto:my-other-app@appspot.gserviceaccount.com%22">my-other-app@appspot.gserviceaccount.com"</a> : An email address that represents a service account.</li>
<li>"group: <a href="mailto:admins@example.com%22">admins@example.com"</a> : An email address that represents a Google group.</li>
<li>"domain:example.com":The Google Workspace domain (primary) that represents all the users of that domain.</li>
<li>"allAuthenticatedUsers": A special identifier that represents all service accounts and all users on the internet who have authenticated with a Google Account. This identifier includes accounts that aren't connected to a Google Workspace or Cloud Identity domain, such as personal Gmail accounts. Users who aren't authenticated, such as anonymous visitors, aren't included.</li>
<li>"allUsers":A special identifier that represents anyone who is on the internet, including authenticated and unauthenticated users. Because BigQuery requires authentication before a user can access the service, allUsers includes only authenticated users.</li>
</ul></td>
</tr>
</tbody>
</table>

## RowAccessPolicyReference

Id path of a row access policy.

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

| Methods                                                                                                                    |                                                                  |
|----------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------|
| [`batchDelete`](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/rowAccessPolicies/batchDelete)               | Deletes provided row access policies.                            |
| [`delete`](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/rowAccessPolicies/delete)                         | Deletes a row access policy.                                     |
| [`get`](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/rowAccessPolicies/get)                               | Gets the specified row access policy by policy ID.               |
| [`getIamPolicy`](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/rowAccessPolicies/getIamPolicy)             | Gets the access control policy for a resource.                   |
| [`insert`](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/rowAccessPolicies/insert)                         | Creates a row access policy.                                     |
| [`list`](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/rowAccessPolicies/list)                             | Lists all row access policies on the specified table.            |
| [`testIamPermissions`](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/rowAccessPolicies/testIamPermissions) | Returns permissions that a caller has on the specified resource. |
| [`update`](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/rowAccessPolicies/update)                         | Updates a row access policy.                                     |
