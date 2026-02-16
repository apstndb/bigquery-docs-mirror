  - [JSON representation](#SCHEMA_REPRESENTATION)
  - [AuditLogConfig](#AuditLogConfig)
      - [JSON representation](#AuditLogConfig.SCHEMA_REPRESENTATION)

Specifies the audit configuration for a service. The configuration determines which permission types are logged, and what identities, if any, are exempted from logging. An AuditConfig must have one or more AuditLogConfigs.

If there are AuditConfigs for both `  allServices  ` and a specific service, the union of the two AuditConfigs is used for that service: the log\_types specified in each AuditConfig are enabled, and the exemptedMembers in each AuditLogConfig are exempted.

Example Policy with multiple AuditConfigs:

``` text
{
  "auditConfigs": [
    {
      "service": "allServices",
      "auditLogConfigs": [
        {
          "logType": "DATA_READ",
          "exemptedMembers": [
            "user:jose@example.com"
          ]
        },
        {
          "logType": "DATA_WRITE"
        },
        {
          "logType": "ADMIN_READ"
        }
      ]
    },
    {
      "service": "sampleservice.googleapis.com",
      "auditLogConfigs": [
        {
          "logType": "DATA_READ"
        },
        {
          "logType": "DATA_WRITE",
          "exemptedMembers": [
            "user:aliya@example.com"
          ]
        }
      ]
    }
  ]
}
```

For sampleservice, this policy enables DATA\_READ, DATA\_WRITE and ADMIN\_READ logging. It also exempts `  jose@example.com  ` from DATA\_READ logging, and `  aliya@example.com  ` from DATA\_WRITE logging.

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
  &quot;service&quot;: string,
  &quot;auditLogConfigs&quot;: [
    {
      object (AuditLogConfig)
    }
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  service  `

`  string  `

Specifies a service that will be enabled for audit logging. For example, `  storage.googleapis.com  ` , `  cloudsql.googleapis.com  ` . `  allServices  ` is a special value that covers all services.

`  auditLogConfigs[]  `

`  object ( AuditLogConfig  ` )

The configuration for logging of each type of permission.

## AuditLogConfig

Provides the configuration for logging a type of permissions. Example:

``` text
{
  "auditLogConfigs": [
    {
      "logType": "DATA_READ",
      "exemptedMembers": [
        "user:jose@example.com"
      ]
    },
    {
      "logType": "DATA_WRITE"
    }
  ]
}
```

This enables 'DATA\_READ' and 'DATA\_WRITE' logging, while exempting <jose@example.com> from DATA\_READ logging.

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
  &quot;logType&quot;: enum (LogType),
  &quot;exemptedMembers&quot;: [
    string
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  logType  `

`  enum ( LogType  ` )

The log type that this config enables.

`  exemptedMembers[]  `

`  string  `

Specifies the identities that do not cause logging for this type of permission. Follows the same format of `  Binding.members  ` .
