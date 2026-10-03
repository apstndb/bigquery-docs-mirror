---
name: documents/docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/Shared.Types/SetIamPolicyRequest
uri: https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/Shared.Types/SetIamPolicyRequest
title: SetIamPolicyRequest
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

- [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/Shared.Types/SetIamPolicyRequest#SCHEMA_REPRESENTATION)

Request message for `SetIamPolicy` method.

**JSON representation**

```
{
  "resource": string,
  "policy": {
    object (Policy)
  },
  "updateMask": string
}
```

| Fields       |                                                                                                                                                                                                                                                                                                                                                                                                                             |
|--------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `resource`   | `string` REQUIRED: The resource for which the policy is being specified. See [Resource names](https://cloud.google.com/apis/design/resource_names) for the appropriate value for this field.                                                                                                                                                                                                                                |
| `policy`     | `object ( `[`Policy`](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/Shared.Types/Policy)` )` REQUIRED: The complete policy to be applied to the `resource` . The size of the policy is limited to a few 10s of KB. An empty policy is a valid policy but certain Google Cloud services (such as Projects) might reject them.                                                                     |
| `updateMask` | `string ( `[`FieldMask`](https://protobuf.dev/reference/protobuf/google.protobuf/#field-mask)` format)` OPTIONAL: A FieldMask specifying which fields of the policy to modify. Only the fields in the mask will be modified. If no mask is provided, the following default mask is used: `paths: "bindings, etag"` This is a comma-separated list of fully qualified names of fields. Example: `"user.displayName,photo"` . |
