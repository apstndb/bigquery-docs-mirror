---
name: documents/docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rest/Shared.Types/Policy
uri: https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rest/Shared.Types/Policy
title: Policy
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

- [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rest/Shared.Types/Policy#SCHEMA_REPRESENTATION)

An Identity and Access Management (IAM) policy, which specifies access controls for Google Cloud resources.

A `Policy` is a collection of `bindings` . A `binding` binds one or more `members` , or principals, to a single `role` . Principals can be user accounts, service accounts, Google groups, and domains (such as G Suite). A `role` is a named list of permissions; each `role` can be an IAM predefined role or a user-created custom role.

For some types of Google Cloud resources, a `binding` can also specify a `condition` , which is a logical expression that allows access to a resource only if the expression evaluates to `true` . A condition can add constraints based on attributes of the request, the resource, or both. To learn which resources support conditions in their IAM policies, see the [IAM documentation](https://cloud.google.com/iam/help/conditions/resource-policies) .

**JSON example:**

```
    {
      "bindings": [
        {
          "role": "roles/resourcemanager.organizationAdmin",
          "members": [
            "user:mike@example.com",
            "group:admins@example.com",
            "domain:google.com",
            "serviceAccount:my-project-id@appspot.gserviceaccount.com"
          ]
        },
        {
          "role": "roles/resourcemanager.organizationViewer",
          "members": [
            "user:eve@example.com"
          ],
          "condition": {
            "title": "expirable access",
            "description": "Does not grant access after Sep 2020",
            "expression": "request.time < timestamp('2020-10-01T00:00:00.000Z')",
          }
        }
      ],
      "etag": "BwWWja0YfJA=",
      "version": 3
    }
```

**YAML example:**

```
    bindings:
    - members:
      - user:mike@example.com
      - group:admins@example.com
      - domain:google.com
      - serviceAccount:my-project-id@appspot.gserviceaccount.com
      role: roles/resourcemanager.organizationAdmin
    - members:
      - user:eve@example.com
      role: roles/resourcemanager.organizationViewer
      condition:
        title: expirable access
        description: Does not grant access after Sep 2020
        expression: request.time < timestamp('2020-10-01T00:00:00.000Z')
    etag: BwWWja0YfJA=
    version: 3
```

For a description of IAM and its features, see the [IAM documentation](https://cloud.google.com/iam/docs/) .

**JSON representation**

```
{
  "version": integer,
  "bindings": [
    {
      object (Binding)
    }
  ],
  "auditConfigs": [
    {
      object (AuditConfig)
    }
  ],
  "etag": string
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
<td><code>version</code></td>
<td><p><code>integer</code></p>
<p>Specifies the format of the policy.</p>
<p>Valid values are <code>0</code> , <code>1</code> , and <code>3</code> . Requests that specify an invalid value are rejected.</p>
<p>Any operation that affects conditional role bindings must specify version <code>3</code> . This requirement applies to the following operations:</p>
<ul>
<li>Getting a policy that includes a conditional role binding</li>
<li>Adding a conditional role binding to a policy</li>
<li>Changing a conditional role binding in a policy</li>
<li>Removing any role binding, with or without a condition, from a policy that includes conditions</li>
</ul>
<p><strong>Important:</strong> If you use IAM Conditions, you must include the <code>etag</code> field whenever you call <code>setIamPolicy</code> . If you omit this field, then IAM allows you to overwrite a version <code>3</code> policy with a version <code>1</code> policy, and all of the conditions in the version <code>3</code> policy are lost.</p>
<p>If a policy does not include any conditions, operations on that policy may specify any valid version or leave the field unset.</p>
<p>To learn which resources support conditions in their IAM policies, see the <a href="https://cloud.google.com/iam/help/conditions/resource-policies">IAM documentation</a> .</p></td>
</tr>
<tr class="even">
<td><code>bindings[]</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rest/Shared.Types/Binding"><code>Binding</code></a><code> )</code></p>
<p>Associates a list of <code>members</code> , or principals, with a <code>role</code> . Optionally, may specify a <code>condition</code> that determines how and when the <code>bindings</code> are applied. Each of the <code>bindings</code> must contain at least one principal.</p>
<p>The <code>bindings</code> in a <code>Policy</code> can refer to up to 1,500 principals; up to 250 of these principals can be Google groups. Each occurrence of a principal counts towards these limits. For example, if the <code>bindings</code> grant 50 different roles to <code>user:alice@example.com</code> , and not to any other principal, then you can add another 1,450 principals to the <code>bindings</code> in the <code>Policy</code> .</p></td>
</tr>
<tr class="odd">
<td><code>auditConfigs[]</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rest/Shared.Types/AuditConfig"><code>AuditConfig</code></a><code> )</code></p>
<p>Specifies cloud audit logging configuration for this policy.</p></td>
</tr>
<tr class="even">
<td><code>etag</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>bytes</code></a><code> format)</code></p>
<p><code>etag</code> is used for optimistic concurrency control as a way to help prevent simultaneous updates of a policy from overwriting each other. It is strongly suggested that systems make use of the <code>etag</code> in the read-modify-write cycle to perform policy updates in order to avoid race conditions: An <code>etag</code> is returned in the response to <code>getIamPolicy</code> , and systems are expected to put that etag in the request to <code>setIamPolicy</code> to ensure that their change will be applied to the same version of the policy.</p>
<p><strong>Important:</strong> If you use IAM Conditions, you must include the <code>etag</code> field whenever you call <code>setIamPolicy</code> . If you omit this field, then IAM allows you to overwrite a version <code>3</code> policy with a version <code>1</code> policy, and all of the conditions in the version <code>3</code> policy are lost.</p></td>
</tr>
</tbody>
</table>
