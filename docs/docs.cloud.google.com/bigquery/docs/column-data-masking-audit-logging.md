# BigQuery Data Policy audit logging

This document describes audit logging for BigQuery Data Policy. Google Cloud services generate audit logs that record administrative and access activities within your Google Cloud resources. For more information about Cloud Audit Logs, see the following:

  - [Types of audit logs](/logging/docs/audit#types)
  - [Audit log entry structure](/logging/docs/audit#audit_log_entry_structure)
  - [Storing and routing audit logs](/logging/docs/audit#storing_and_routing_audit_logs)
  - [Cloud Logging pricing summary](/stackdriver/pricing#logs-pricing-summary)
  - [Enable Data Access audit logs](/logging/docs/audit/configure-data-access)

## Service name

BigQuery Data Policy audit logs use the service name `  bigquerydatapolicy.googleapis.com  ` . Filter for this service:

``` text
    protoPayload.serviceName="bigquerydatapolicy.googleapis.com"
  
```

## Methods by permission type

Each IAM permission has a `  type  ` property, whose value is an enum that can be one of four values: `  ADMIN_READ  ` , `  ADMIN_WRITE  ` , `  DATA_READ  ` , or `  DATA_WRITE  ` . When you call a method, BigQuery Data Policy generates an audit log whose category is dependent on the `  type  ` property of the permission required to perform the method. Methods that require an IAM permission with the `  type  ` property value of `  DATA_READ  ` , `  DATA_WRITE  ` , or `  ADMIN_READ  ` generate [Data Access](/logging/docs/audit#data-access) audit logs. Methods that require an IAM permission with the `  type  ` property value of `  ADMIN_WRITE  ` generate [Admin Activity](/logging/docs/audit#admin-activity) audit logs.

API methods in the following list that are marked with (LRO) are long-running operations (LROs). These methods usually generate two audit log entries: one when the operation starts and another when it ends. For more information see [Audit logs for long-running operations](/logging/docs/audit/understanding-audit-logs#lro) .

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Permission type</th>
<th>Methods</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       ADMIN_READ      </code></td>
<td><code dir="ltr" translate="no">       google.cloud.bigquery.datapolicies.v1.DataPolicyService.GetDataPolicy      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.datapolicies.v1.DataPolicyService.GetIamPolicy      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.datapolicies.v1.DataPolicyService.ListDataPolicies      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.datapolicies.v1beta1.DataPolicyService.GetDataPolicy      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.datapolicies.v1beta1.DataPolicyService.GetIamPolicy      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.datapolicies.v1beta1.DataPolicyService.ListDataPolicies      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       ADMIN_WRITE      </code></td>
<td><code dir="ltr" translate="no">       google.cloud.bigquery.datapolicies.v1.DataPolicyService.CreateDataPolicy      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.datapolicies.v1.DataPolicyService.DeleteDataPolicy      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.datapolicies.v1.DataPolicyService.RenameDataPolicy      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.datapolicies.v1.DataPolicyService.SetIamPolicy      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.datapolicies.v1.DataPolicyService.UpdateDataPolicy      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.datapolicies.v1beta1.DataPolicyService.CreateDataPolicy      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.datapolicies.v1beta1.DataPolicyService.DeleteDataPolicy      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.datapolicies.v1beta1.DataPolicyService.SetIamPolicy      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.datapolicies.v1beta1.DataPolicyService.UpdateDataPolicy      </code></td>
</tr>
</tbody>
</table>

## API interface audit logs

For information about how and which permissions are evaluated for each method, see the Identity and Access Management documentation for BigQuery Data Policy.

### `     google.cloud.bigquery.datapolicies.v1.DataPolicyService    `

The following audit logs are associated with methods belonging to `  google.cloud.bigquery.datapolicies.v1.DataPolicyService  ` .

#### `     CreateDataPolicy    `

  - **Method** : `  google.cloud.bigquery.datapolicies.v1.DataPolicyService.CreateDataPolicy  `  
  - **Audit log type** : [Admin activity](/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `  bigquery.dataPolicies.create - ADMIN_WRITE  `
      - `  datacatalog.taxonomies.get - ADMIN_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.datapolicies.v1.DataPolicyService.CreateDataPolicy"  `  

#### `     DeleteDataPolicy    `

  - **Method** : `  google.cloud.bigquery.datapolicies.v1.DataPolicyService.DeleteDataPolicy  `  
  - **Audit log type** : [Admin activity](/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `  bigquery.dataPolicies.delete - ADMIN_WRITE  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.datapolicies.v1.DataPolicyService.DeleteDataPolicy"  `  

#### `     GetDataPolicy    `

  - **Method** : `  google.cloud.bigquery.datapolicies.v1.DataPolicyService.GetDataPolicy  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  bigquery.dataPolicies.get - ADMIN_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.datapolicies.v1.DataPolicyService.GetDataPolicy"  `  

#### `     GetIamPolicy    `

  - **Method** : `  google.cloud.bigquery.datapolicies.v1.DataPolicyService.GetIamPolicy  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  bigquery.dataPolicies.getIamPolicy - ADMIN_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.datapolicies.v1.DataPolicyService.GetIamPolicy"  `  

#### `     ListDataPolicies    `

  - **Method** : `  google.cloud.bigquery.datapolicies.v1.DataPolicyService.ListDataPolicies  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  bigquery.dataPolicies.list - ADMIN_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.datapolicies.v1.DataPolicyService.ListDataPolicies"  `  

#### `     RenameDataPolicy    `

  - **Method** : `  google.cloud.bigquery.datapolicies.v1.DataPolicyService.RenameDataPolicy  `  
  - **Audit log type** : [Admin activity](/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `  bigquery.dataPolicies.update - ADMIN_WRITE  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.datapolicies.v1.DataPolicyService.RenameDataPolicy"  `  

#### `     SetIamPolicy    `

  - **Method** : `  google.cloud.bigquery.datapolicies.v1.DataPolicyService.SetIamPolicy  `  
  - **Audit log type** : [Admin activity](/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `  bigquery.dataPolicies.setIamPolicy - ADMIN_WRITE  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.datapolicies.v1.DataPolicyService.SetIamPolicy"  `  

#### `     UpdateDataPolicy    `

  - **Method** : `  google.cloud.bigquery.datapolicies.v1.DataPolicyService.UpdateDataPolicy  `  
  - **Audit log type** : [Admin activity](/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `  bigquery.dataPolicies.update - ADMIN_WRITE  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.datapolicies.v1.DataPolicyService.UpdateDataPolicy"  `  

### `     google.cloud.bigquery.datapolicies.v1beta1.DataPolicyService    `

The following audit logs are associated with methods belonging to `  google.cloud.bigquery.datapolicies.v1beta1.DataPolicyService  ` .

#### `     CreateDataPolicy    `

  - **Method** : `  google.cloud.bigquery.datapolicies.v1beta1.DataPolicyService.CreateDataPolicy  `  
  - **Audit log type** : [Admin activity](/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `  bigquery.dataPolicies.create - ADMIN_WRITE  `
      - `  datacatalog.taxonomies.get - ADMIN_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.datapolicies.v1beta1.DataPolicyService.CreateDataPolicy"  `  

#### `     DeleteDataPolicy    `

  - **Method** : `  google.cloud.bigquery.datapolicies.v1beta1.DataPolicyService.DeleteDataPolicy  `  
  - **Audit log type** : [Admin activity](/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `  bigquery.dataPolicies.delete - ADMIN_WRITE  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.datapolicies.v1beta1.DataPolicyService.DeleteDataPolicy"  `  

#### `     GetDataPolicy    `

  - **Method** : `  google.cloud.bigquery.datapolicies.v1beta1.DataPolicyService.GetDataPolicy  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  bigquery.dataPolicies.get - ADMIN_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.datapolicies.v1beta1.DataPolicyService.GetDataPolicy"  `  

#### `     GetIamPolicy    `

  - **Method** : `  google.cloud.bigquery.datapolicies.v1beta1.DataPolicyService.GetIamPolicy  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  bigquery.dataPolicies.getIamPolicy - ADMIN_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.datapolicies.v1beta1.DataPolicyService.GetIamPolicy"  `  

#### `     ListDataPolicies    `

  - **Method** : `  google.cloud.bigquery.datapolicies.v1beta1.DataPolicyService.ListDataPolicies  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  bigquery.dataPolicies.list - ADMIN_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.datapolicies.v1beta1.DataPolicyService.ListDataPolicies"  `  

#### `     SetIamPolicy    `

  - **Method** : `  google.cloud.bigquery.datapolicies.v1beta1.DataPolicyService.SetIamPolicy  `  
  - **Audit log type** : [Admin activity](/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `  bigquery.dataPolicies.setIamPolicy - ADMIN_WRITE  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.datapolicies.v1beta1.DataPolicyService.SetIamPolicy"  `  

#### `     UpdateDataPolicy    `

  - **Method** : `  google.cloud.bigquery.datapolicies.v1beta1.DataPolicyService.UpdateDataPolicy  `  
  - **Audit log type** : [Admin activity](/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `  bigquery.dataPolicies.update - ADMIN_WRITE  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.datapolicies.v1beta1.DataPolicyService.UpdateDataPolicy"  `  

## Methods that don't produce audit logs

A method might not produce audit logs for one or more of the following reasons:

  - It is a high volume method involving significant log generation and storage costs.
  - It has low auditing value.
  - Another audit or platform log already provides method coverage.

The following methods don't produce audit logs:

  - `  google.cloud.bigquery.datapolicies.v1.DataPolicyService.TestIamPermissions  `
  - `  google.cloud.bigquery.datapolicies.v1beta1.DataPolicyService.TestIamPermissions  `
