---
name: documents/docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/Shared.Types/Binding
uri: https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/Shared.Types/Binding
title: Binding
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

- [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/Shared.Types/Binding#SCHEMA_REPRESENTATION)
- [Expr](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/Shared.Types/Binding#Expr)
  - [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/Shared.Types/Binding#Expr.SCHEMA_REPRESENTATION)

Associates `members` , or principals, with a `role` .

**JSON representation**

```
{
  "role": string,
  "members": [
    string
  ],
  "condition": {
    object (Expr)
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
<td><code>role</code></td>
<td><p><code>string</code></p>
<p>Role that is assigned to the list of <code>members</code> , or principals. For example, <code>roles/viewer</code> , <code>roles/editor</code> , or <code>roles/owner</code> .</p>
<p>For an overview of the IAM roles and permissions, see the <a href="https://cloud.google.com/iam/docs/roles-overview">IAM documentation</a> . For a list of the available pre-defined roles, see <a href="https://cloud.google.com/iam/docs/understanding-roles">here</a> .</p></td>
</tr>
<tr class="even">
<td><code>members[]</code></td>
<td><p><code>string</code></p>
<p>Specifies the principals requesting access for a Google Cloud resource. <code>members</code> can have the following values:</p>
<ul>
<li><p><code>allUsers</code> : A special identifier that represents anyone who is on the internet; with or without a Google account.</p></li>
<li><p><code>allAuthenticatedUsers</code> : A special identifier that represents anyone who is authenticated with a Google account or a service account. Does not include identities that come from external identity providers (IdPs) through identity federation.</p></li>
<li><p><code>user:{emailid}</code> : An email address that represents a specific Google account. For example, <code>alice@example.com</code> .</p></li>
</ul>
<ul>
<li><p><code>serviceAccount:{emailid}</code> : An email address that represents a Google service account. For example, <code>my-other-app@appspot.gserviceaccount.com</code> .</p></li>
<li><p><code>serviceAccount:{projectid}.svc.id.goog[{namespace}/{kubernetes-sa}]</code> : An identifier for a <a href="https://cloud.google.com/kubernetes-engine/docs/how-to/kubernetes-service-accounts">Kubernetes service account</a> . For example, <code>my-project.svc.id.goog[my-namespace/my-kubernetes-sa]</code> .</p></li>
<li><p><code>group:{emailid}</code> : An email address that represents a Google group. For example, <code>admins@example.com</code> .</p></li>
</ul>
<ul>
<li><code>domain:{domain}</code> : The G Suite domain (primary) that represents all the users of that domain. For example, <code>google.com</code> or <code>example.com</code> .</li>
</ul>
<ul>
<li><p><code>principal://iam.googleapis.com/locations/global/workforcePools/{pool_id}/subject/{subject_attribute_value}</code> : A single identity in a workforce identity pool.</p></li>
<li><p><code>principalSet://iam.googleapis.com/locations/global/workforcePools/{pool_id}/group/{groupId}</code> : All workforce identities in a group.</p></li>
<li><p><code>principalSet://iam.googleapis.com/locations/global/workforcePools/{pool_id}/attribute.{attribute_name}/{attribute_value}</code> : All workforce identities with a specific attribute value.</p></li>
<li><p><code>principalSet://iam.googleapis.com/locations/global/workforcePools/{pool_id}/*</code> : All identities in a workforce identity pool.</p></li>
<li><p><code>principal://iam.googleapis.com/projects/{projectNumber}/locations/global/workloadIdentityPools/{pool_id}/subject/{subject_attribute_value}</code> : A single identity in a workload identity pool.</p></li>
<li><p><code>principalSet://iam.googleapis.com/projects/{projectNumber}/locations/global/workloadIdentityPools/{pool_id}/group/{groupId}</code> : A workload identity pool group.</p></li>
<li><p><code>principalSet://iam.googleapis.com/projects/{projectNumber}/locations/global/workloadIdentityPools/{pool_id}/attribute.{attribute_name}/{attribute_value}</code> : All identities in a workload identity pool with a certain attribute.</p></li>
<li><p><code>principalSet://iam.googleapis.com/projects/{projectNumber}/locations/global/workloadIdentityPools/{pool_id}/*</code> : All identities in a workload identity pool.</p></li>
<li><p><code>deleted:user:{emailid}?uid={uniqueid}</code> : An email address (plus unique identifier) representing a user that has been recently deleted. For example, <code>alice@example.com?uid=123456789012345678901</code> . If the user is recovered, this value reverts to <code>user:{emailid}</code> and the recovered user retains the role in the binding.</p></li>
<li><p><code>deleted:serviceAccount:{emailid}?uid={uniqueid}</code> : An email address (plus unique identifier) representing a service account that has been recently deleted. For example, <code>my-other-app@appspot.gserviceaccount.com?uid=123456789012345678901</code> . If the service account is undeleted, this value reverts to <code>serviceAccount:{emailid}</code> and the undeleted service account retains the role in the binding.</p></li>
<li><p><code>deleted:group:{emailid}?uid={uniqueid}</code> : An email address (plus unique identifier) representing a Google group that has been recently deleted. For example, <code>admins@example.com?uid=123456789012345678901</code> . If the group is recovered, this value reverts to <code>group:{emailid}</code> and the recovered group retains the role in the binding.</p></li>
<li><p><code>deleted:principal://iam.googleapis.com/locations/global/workforcePools/{pool_id}/subject/{subject_attribute_value}</code> : Deleted single identity in a workforce identity pool. For example, <code>deleted:principal://iam.googleapis.com/locations/global/workforcePools/my-pool-id/subject/my-subject-attribute-value</code> .</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><code>condition</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/Shared.Types/Binding#Expr"><code>Expr</code></a><code> )</code></p>
<p>The condition that is associated with this binding.</p>
<p>If the condition evaluates to <code>true</code> , then this binding applies to the current request.</p>
<p>If the condition evaluates to <code>false</code> , then this binding does not apply to the current request. However, a different role binding might grant the same role to one or more of the principals in this binding.</p>
<p>To learn which resources support conditions in their IAM policies, see the <a href="https://cloud.google.com/iam/help/conditions/resource-policies">IAM documentation</a> .</p></td>
</tr>
</tbody>
</table>

## Expr

Represents a textual expression in the Common Expression Language (CEL) syntax. CEL is a C-like expression language. The syntax and semantics of CEL are documented at <https://github.com/google/cel-spec> .

Example (Comparison):

```
title: "Summary size limit"
description: "Determines if a summary is less than 100 chars"
expression: "document.summary.size() < 100"
```

Example (Equality):

```
title: "Requestor is owner"
description: "Determines if requestor is the document owner"
expression: "document.owner == request.auth.claims.email"
```

Example (Logic):

```
title: "Public documents"
description: "Determine whether the document should be publicly visible"
expression: "document.type != 'private' && document.type != 'internal'"
```

Example (Data Manipulation):

```
title: "Notification string"
description: "Create a notification string with a timestamp."
expression: "'New message received at ' + string(document.create_time)"
```

The exact variables and functions that may be referenced within an expression are determined by the service that evaluates it. See the service documentation for additional information.

**JSON representation**

```
{
  "expression": string,
  "title": string,
  "description": string,
  "location": string
}
```

| Fields        |                                                                                                                                                            |
|---------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `expression`  | `string` Textual representation of an expression in Common Expression Language syntax.                                                                     |
| `title`       | `string` Optional. Title for the expression, i.e. a short string describing its purpose. This can be used e.g. in UIs which allow to enter the expression. |
| `description` | `string` Optional. Description of the expression. This is a longer text which describes the expression, e.g. when hovered over it in a UI.                 |
| `location`    | `string` Optional. String indicating the location of the expression for error reporting, e.g. a file name and a position in the file.                      |
