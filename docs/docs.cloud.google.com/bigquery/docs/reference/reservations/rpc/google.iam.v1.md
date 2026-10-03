---
name: documents/docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.iam.v1
uri: https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.iam.v1
title: Package google.iam.v1
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

## Index

- [`AuditConfig`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.iam.v1#google.iam.v1.AuditConfig) (message)
- [`AuditLogConfig`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.iam.v1#google.iam.v1.AuditLogConfig) (message)
- [`AuditLogConfig.LogType`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.iam.v1#google.iam.v1.AuditLogConfig.LogType) (enum)
- [`Binding`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.iam.v1#google.iam.v1.Binding) (message)
- [`GetIamPolicyRequest`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.iam.v1#google.iam.v1.GetIamPolicyRequest) (message)
- [`GetPolicyOptions`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.iam.v1#google.iam.v1.GetPolicyOptions) (message)
- [`Policy`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.iam.v1#google.iam.v1.Policy) (message)
- [`SetIamPolicyRequest`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.iam.v1#google.iam.v1.SetIamPolicyRequest) (message)
- [`TestIamPermissionsRequest`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.iam.v1#google.iam.v1.TestIamPermissionsRequest) (message)
- [`TestIamPermissionsResponse`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.iam.v1#google.iam.v1.TestIamPermissionsResponse) (message)

## AuditConfig

Specifies the audit configuration for a service. The configuration determines which permission types are logged, and what identities, if any, are exempted from logging. An AuditConfig must have one or more AuditLogConfigs.

If there are AuditConfigs for both `allServices` and a specific service, the union of the two AuditConfigs is used for that service: the log_types specified in each AuditConfig are enabled, and the exempted_members in each AuditLogConfig are exempted.

Example Policy with multiple AuditConfigs:

```
{
  "audit_configs": [
    {
      "service": "allServices",
      "audit_log_configs": [
        {
          "log_type": "DATA_READ",
          "exempted_members": [
            "user:jose@example.com"
          ]
        },
        {
          "log_type": "DATA_WRITE"
        },
        {
          "log_type": "ADMIN_READ"
        }
      ]
    },
    {
      "service": "sampleservice.googleapis.com",
      "audit_log_configs": [
        {
          "log_type": "DATA_READ"
        },
        {
          "log_type": "DATA_WRITE",
          "exempted_members": [
            "user:aliya@example.com"
          ]
        }
      ]
    }
  ]
}
```

For sampleservice, this policy enables DATA_READ, DATA_WRITE and ADMIN_READ logging. It also exempts `jose@example.com` from DATA_READ logging, and `aliya@example.com` from DATA_WRITE logging.

| Fields                |                                                                                                                                                                                                     |
|-----------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `service`             | `string` Specifies a service that will be enabled for audit logging. For example, `storage.googleapis.com` , `cloudsql.googleapis.com` . `allServices` is a special value that covers all services. |
| `audit_log_configs[]` | [`AuditLogConfig`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.iam.v1#google.iam.v1.AuditLogConfig) The configuration for logging of each type of permission.     |

## AuditLogConfig

Provides the configuration for logging a type of permissions. Example:

```
{
  "audit_log_configs": [
    {
      "log_type": "DATA_READ",
      "exempted_members": [
        "user:jose@example.com"
      ]
    },
    {
      "log_type": "DATA_WRITE"
    }
  ]
}
```

This enables 'DATA_READ' and 'DATA_WRITE' logging, while exempting <jose@example.com> from DATA_READ logging.

| Fields               |                                                                                                                                                                                                                                                                                                            |
|----------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `log_type`           | [`LogType`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.iam.v1#google.iam.v1.AuditLogConfig.LogType) The log type that this config enables.                                                                                                                              |
| `exempted_members[]` | `string` Specifies the identities that do not cause logging for this type of permission. Follows the same format of [`Binding.members`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.iam.v1#google.iam.v1.Binding.FIELDS.repeated.string.google.iam.v1.Binding.members) . |

## LogType

The list of valid permission types for which logging can be configured. Admin writes are always logged, and are not configurable.

| Enums                  |                                             |
|------------------------|---------------------------------------------|
| `LOG_TYPE_UNSPECIFIED` | Default case. Should never be this.         |
| `ADMIN_READ`           | Admin reads. Example: CloudIAM getIamPolicy |
| `DATA_WRITE`           | Data writes. Example: CloudSQL Users create |
| `DATA_READ`            | Data reads. Example: CloudSQL Users list    |

## Binding

Associates `members` , or principals, with a `role` .

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
<li><p><code>principalSet://iam.googleapis.com/locations/global/workforcePools/{pool_id}/group/{group_id}</code> : All workforce identities in a group.</p></li>
<li><p><code>principalSet://iam.googleapis.com/locations/global/workforcePools/{pool_id}/attribute.{attribute_name}/{attribute_value}</code> : All workforce identities with a specific attribute value.</p></li>
<li><p><code>principalSet://iam.googleapis.com/locations/global/workforcePools/{pool_id}/*</code> : All identities in a workforce identity pool.</p></li>
<li><p><code>principal://iam.googleapis.com/projects/{project_number}/locations/global/workloadIdentityPools/{pool_id}/subject/{subject_attribute_value}</code> : A single identity in a workload identity pool.</p></li>
<li><p><code>principalSet://iam.googleapis.com/projects/{project_number}/locations/global/workloadIdentityPools/{pool_id}/group/{group_id}</code> : A workload identity pool group.</p></li>
<li><p><code>principalSet://iam.googleapis.com/projects/{project_number}/locations/global/workloadIdentityPools/{pool_id}/attribute.{attribute_name}/{attribute_value}</code> : All identities in a workload identity pool with a certain attribute.</p></li>
<li><p><code>principalSet://iam.googleapis.com/projects/{project_number}/locations/global/workloadIdentityPools/{pool_id}/*</code> : All identities in a workload identity pool.</p></li>
<li><p><code>deleted:user:{emailid}?uid={uniqueid}</code> : An email address (plus unique identifier) representing a user that has been recently deleted. For example, <code>alice@example.com?uid=123456789012345678901</code> . If the user is recovered, this value reverts to <code>user:{emailid}</code> and the recovered user retains the role in the binding.</p></li>
<li><p><code>deleted:serviceAccount:{emailid}?uid={uniqueid}</code> : An email address (plus unique identifier) representing a service account that has been recently deleted. For example, <code>my-other-app@appspot.gserviceaccount.com?uid=123456789012345678901</code> . If the service account is undeleted, this value reverts to <code>serviceAccount:{emailid}</code> and the undeleted service account retains the role in the binding.</p></li>
<li><p><code>deleted:group:{emailid}?uid={uniqueid}</code> : An email address (plus unique identifier) representing a Google group that has been recently deleted. For example, <code>admins@example.com?uid=123456789012345678901</code> . If the group is recovered, this value reverts to <code>group:{emailid}</code> and the recovered group retains the role in the binding.</p></li>
<li><p><code>deleted:principal://iam.googleapis.com/locations/global/workforcePools/{pool_id}/subject/{subject_attribute_value}</code> : Deleted single identity in a workforce identity pool. For example, <code>deleted:principal://iam.googleapis.com/locations/global/workforcePools/my-pool-id/subject/my-subject-attribute-value</code> .</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><code>condition</code></td>
<td><p><a href="https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.type#google.type.Expr"><code>Expr</code></a></p>
<p>The condition that is associated with this binding.</p>
<p>If the condition evaluates to <code>true</code> , then this binding applies to the current request.</p>
<p>If the condition evaluates to <code>false</code> , then this binding does not apply to the current request. However, a different role binding might grant the same role to one or more of the principals in this binding.</p>
<p>To learn which resources support conditions in their IAM policies, see the <a href="https://cloud.google.com/iam/help/conditions/resource-policies">IAM documentation</a> .</p></td>
</tr>
</tbody>
</table>

## GetIamPolicyRequest

Request message for `GetIamPolicy` method.

| Fields     |                                                                                                                                                                                                                            |
|------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `resource` | `string` REQUIRED: The resource for which the policy is being requested. See [Resource names](https://cloud.google.com/apis/design/resource_names) for the appropriate value for this field.                               |
| `options`  | [`GetPolicyOptions`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.iam.v1#google.iam.v1.GetPolicyOptions) OPTIONAL: A `GetPolicyOptions` object for specifying options to `GetIamPolicy` . |

## GetPolicyOptions

Encapsulates settings provided to GetIamPolicy.

| Fields                     |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
|----------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `requested_policy_version` | `int32` Optional. The maximum policy version that will be used to format the policy. Valid values are 0, 1, and 3. Requests specifying an invalid value will be rejected. Requests for policies with any conditional role bindings must specify version 3. Policies with no conditional role bindings may specify any valid value or leave the field unset. The policy in the response might use the policy version that you specified, or it might use a lower policy version. For example, if you specify version 3, but the policy has no conditional role bindings, the response uses version 1. To learn which resources support conditions in their IAM policies, see the [IAM documentation](https://cloud.google.com/iam/help/conditions/resource-policies) . |

## Policy

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
<td><p><code>int32</code></p>
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
<td><p><a href="https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.iam.v1#google.iam.v1.Binding"><code>Binding</code></a></p>
<p>Associates a list of <code>members</code> , or principals, with a <code>role</code> . Optionally, may specify a <code>condition</code> that determines how and when the <code>bindings</code> are applied. Each of the <code>bindings</code> must contain at least one principal.</p>
<p>The <code>bindings</code> in a <code>Policy</code> can refer to up to 1,500 principals; up to 250 of these principals can be Google groups. Each occurrence of a principal counts towards these limits. For example, if the <code>bindings</code> grant 50 different roles to <code>user:alice@example.com</code> , and not to any other principal, then you can add another 1,450 principals to the <code>bindings</code> in the <code>Policy</code> .</p></td>
</tr>
<tr class="odd">
<td><code>audit_configs[]</code></td>
<td><p><a href="https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.iam.v1#google.iam.v1.AuditConfig"><code>AuditConfig</code></a></p>
<p>Specifies cloud audit logging configuration for this policy.</p></td>
</tr>
<tr class="even">
<td><code>etag</code></td>
<td><p><code>bytes</code></p>
<p><code>etag</code> is used for optimistic concurrency control as a way to help prevent simultaneous updates of a policy from overwriting each other. It is strongly suggested that systems make use of the <code>etag</code> in the read-modify-write cycle to perform policy updates in order to avoid race conditions: An <code>etag</code> is returned in the response to <code>getIamPolicy</code> , and systems are expected to put that etag in the request to <code>setIamPolicy</code> to ensure that their change will be applied to the same version of the policy.</p>
<p><strong>Important:</strong> If you use IAM Conditions, you must include the <code>etag</code> field whenever you call <code>setIamPolicy</code> . If you omit this field, then IAM allows you to overwrite a version <code>3</code> policy with a version <code>1</code> policy, and all of the conditions in the version <code>3</code> policy are lost.</p></td>
</tr>
</tbody>
</table>

## SetIamPolicyRequest

Request message for `SetIamPolicy` method.

| Fields        |                                                                                                                                                                                                                                                                                                                                                       |
|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `resource`    | `string` REQUIRED: The resource for which the policy is being specified. See [Resource names](https://cloud.google.com/apis/design/resource_names) for the appropriate value for this field.                                                                                                                                                          |
| `policy`      | [`Policy`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc/google.iam.v1#google.iam.v1.Policy) REQUIRED: The complete policy to be applied to the `resource` . The size of the policy is limited to a few 10s of KB. An empty policy is a valid policy but certain Google Cloud services (such as Projects) might reject them. |
| `update_mask` | [`FieldMask`](https://protobuf.dev/reference/protobuf/google.protobuf/#field-mask) OPTIONAL: A FieldMask specifying which fields of the policy to modify. Only the fields in the mask will be modified. If no mask is provided, the following default mask is used: `paths: "bindings, etag"`                                                         |

## TestIamPermissionsRequest

Request message for `TestIamPermissions` method.

| Fields          |                                                                                                                                                                                                                                           |
|-----------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `resource`      | `string` REQUIRED: The resource for which the policy detail is being requested. See [Resource names](https://cloud.google.com/apis/design/resource_names) for the appropriate value for this field.                                       |
| `permissions[]` | `string` The set of permissions to check for the `resource` . Permissions with wildcards (such as `*` or `storage.*` ) are not allowed. For more information see [IAM Overview](https://cloud.google.com/iam/docs/overview#permissions) . |

## TestIamPermissionsResponse

Response message for `TestIamPermissions` method.

| Fields          |                                                                                       |
|-----------------|---------------------------------------------------------------------------------------|
| `permissions[]` | `string` A subset of `TestPermissionsRequest.permissions` that the caller is allowed. |
