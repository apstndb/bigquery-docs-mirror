  - [Resource: RowAccessPolicy](#RowAccessPolicy)
      - [JSON representation](#RowAccessPolicy.SCHEMA_REPRESENTATION)
  - [RowAccessPolicyReference](#RowAccessPolicyReference)
      - [JSON representation](#RowAccessPolicyReference.SCHEMA_REPRESENTATION)
  - [Methods](#METHODS_SUMMARY)

## Resource: RowAccessPolicy

Represents access on a subset of rows on the specified table, defined by its filter predicate. Access to the subset of rows is controlled by its IAM policy.

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
  &quot;etag&quot;: string,
  &quot;rowAccessPolicyReference&quot;: {
    object (RowAccessPolicyReference)
  },
  &quot;filterPredicate&quot;: string,
  &quot;creationTime&quot;: string,
  &quot;lastModifiedTime&quot;: string,
  &quot;grantees&quot;: [
    string
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  etag  `

`  string  `

Output only. A hash of this resource.

`  rowAccessPolicyReference  `

`  object ( RowAccessPolicyReference  ` )

Required. Reference describing the ID of this row access policy.

`  filterPredicate  `

`  string  `

Required. A SQL boolean expression that represents the rows defined by this row access policy, similar to the boolean expression in a WHERE clause of a SELECT query on a table. References to other tables, routines, and temporary functions are not supported.

Examples: region="EU" date\_field = CAST('2019-9-27' as DATE) nullable\_field is not NULL numeric\_field BETWEEN 1.0 AND 5.0

`  creationTime  `

`  string ( Timestamp  ` format)

Output only. The time when this row access policy was created, in milliseconds since the epoch.

`  lastModifiedTime  `

`  string ( Timestamp  ` format)

Output only. The time when this row access policy was last modified, in milliseconds since the epoch.

`  grantees[]  `

`  string  `

Optional. Input only. The optional list of iamMember users or groups that specifies the initial members that the row-level access policy should be created with.

grantees types:

  - "user: [alice@example.com"](mailto:alice@example.com%22) : An email address that represents a specific Google account.
  - "serviceAccount: [my-other-app@appspot.gserviceaccount.com"](mailto:my-other-app@appspot.gserviceaccount.com%22) : An email address that represents a service account.
  - "group: [admins@example.com"](mailto:admins@example.com%22) : An email address that represents a Google group.
  - "domain:example.com":The Google Workspace domain (primary) that represents all the users of that domain.
  - "allAuthenticatedUsers": A special identifier that represents all service accounts and all users on the internet who have authenticated with a Google Account. This identifier includes accounts that aren't connected to a Google Workspace or Cloud Identity domain, such as personal Gmail accounts. Users who aren't authenticated, such as anonymous visitors, aren't included.
  - "allUsers":A special identifier that represents anyone who is on the internet, including authenticated and unauthenticated users. Because BigQuery requires authentication before a user can access the service, allUsers includes only authenticated users.

## RowAccessPolicyReference

Id path of a row access policy.

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
  &quot;datasetId&quot;: string,
  &quot;tableId&quot;: string,
  &quot;policyId&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  projectId  `

`  string  `

Required. The ID of the project containing this row access policy.

`  datasetId  `

`  string  `

Required. The ID of the dataset containing this row access policy.

`  tableId  `

`  string  `

Required. The ID of the table containing this row access policy.

`  policyId  `

`  string  `

Required. The ID of the row access policy. The ID must contain only letters (a-z, A-Z), numbers (0-9), or underscores (\_). The maximum length is 256 characters.

## Methods

### `             batchDelete           `

Deletes provided row access policies.

### `             delete           `

Deletes a row access policy.

### `             get           `

Gets the specified row access policy by policy ID.

### `             getIamPolicy           `

Gets the access control policy for a resource.

### `             insert           `

Creates a row access policy.

### `             list           `

Lists all row access policies on the specified table.

### `             testIamPermissions           `

Returns permissions that a caller has on the specified resource.

### `             update           `

Updates a row access policy.
