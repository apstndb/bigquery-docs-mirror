# BigQuery Migration Service audit logging

This document describes audit logging for BigQuery Migration Service. Google Cloud services generate audit logs that record administrative and access activities within your Google Cloud resources. For more information about Cloud Audit Logs, see the following:

  - [Types of audit logs](/logging/docs/audit#types)
  - [Audit log entry structure](/logging/docs/audit#audit_log_entry_structure)
  - [Storing and routing audit logs](/logging/docs/audit#storing_and_routing_audit_logs)
  - [Cloud Logging pricing summary](/stackdriver/pricing#logs-pricing-summary)
  - [Enable Data Access audit logs](/logging/docs/audit/configure-data-access)

## Service name

BigQuery Migration Service audit logs use the service name `  bigquerymigration.googleapis.com  ` . Filter for this service:

``` text
    protoPayload.serviceName="bigquerymigration.googleapis.com"
  
```

## Methods by permission type

Each IAM permission has a `  type  ` property, whose value is an enum that can be one of four values: `  ADMIN_READ  ` , `  ADMIN_WRITE  ` , `  DATA_READ  ` , or `  DATA_WRITE  ` . When you call a method, BigQuery Migration Service generates an audit log whose category is dependent on the `  type  ` property of the permission required to perform the method. Methods that require an IAM permission with the `  type  ` property value of `  DATA_READ  ` , `  DATA_WRITE  ` , or `  ADMIN_READ  ` generate [Data Access](/logging/docs/audit#data-access) audit logs. Methods that require an IAM permission with the `  type  ` property value of `  ADMIN_WRITE  ` generate [Admin Activity](/logging/docs/audit#admin-activity) audit logs.

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
<td><code dir="ltr" translate="no">       DATA_READ      </code></td>
<td><code dir="ltr" translate="no">       google.cloud.bigquery.migration.v2.MigrationService.GetMigrationSubtask      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.migration.v2.MigrationService.GetMigrationWorkflow      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.migration.v2.MigrationService.ListMigrationSubtasks      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.migration.v2.MigrationService.ListMigrationWorkflows      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.migration.v2.SqlTranslationService.TranslateQuery      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.migration.v2alpha.MigrationService.GetMigrationSubtask      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.migration.v2alpha.MigrationService.GetMigrationWorkflow      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.migration.v2alpha.MigrationService.ListMigrationSubtasks      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.migration.v2alpha.MigrationService.ListMigrationWorkflows      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.migration.v2alpha.SqlTranslationService.TranslateQuery      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       DATA_WRITE      </code></td>
<td><code dir="ltr" translate="no">       google.cloud.bigquery.migration.v2.MigrationService.CreateMigrationWorkflow      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.migration.v2.MigrationService.DeleteMigrationWorkflow      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.migration.v2.MigrationService.StartMigrationWorkflow      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.migration.v2alpha.MigrationService.CreateMigrationWorkflow      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.migration.v2alpha.MigrationService.DeleteMigrationWorkflow      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.migration.v2alpha.MigrationService.StartMigrationWorkflow      </code></td>
</tr>
</tbody>
</table>

## API interface audit logs

For information about how and which permissions are evaluated for each method, see the Identity and Access Management documentation for BigQuery Migration Service.

### `     google.cloud.bigquery.migration.v2.MigrationService    `

The following audit logs are associated with methods belonging to `  google.cloud.bigquery.migration.v2.MigrationService  ` .

#### `     CreateMigrationWorkflow    `

  - **Method** : `  google.cloud.bigquery.migration.v2.MigrationService.CreateMigrationWorkflow  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  bigquerymigration.workflows.create - DATA_WRITE  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.migration.v2.MigrationService.CreateMigrationWorkflow"  `  

#### `     DeleteMigrationWorkflow    `

  - **Method** : `  google.cloud.bigquery.migration.v2.MigrationService.DeleteMigrationWorkflow  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  bigquerymigration.workflows.delete - DATA_WRITE  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.migration.v2.MigrationService.DeleteMigrationWorkflow"  `  

#### `     GetMigrationSubtask    `

  - **Method** : `  google.cloud.bigquery.migration.v2.MigrationService.GetMigrationSubtask  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  bigquerymigration.subtasks.get - DATA_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.migration.v2.MigrationService.GetMigrationSubtask"  `  

#### `     GetMigrationWorkflow    `

  - **Method** : `  google.cloud.bigquery.migration.v2.MigrationService.GetMigrationWorkflow  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  bigquerymigration.workflows.get - DATA_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.migration.v2.MigrationService.GetMigrationWorkflow"  `  

#### `     ListMigrationSubtasks    `

  - **Method** : `  google.cloud.bigquery.migration.v2.MigrationService.ListMigrationSubtasks  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  bigquerymigration.subtasks.list - DATA_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.migration.v2.MigrationService.ListMigrationSubtasks"  `  

#### `     ListMigrationWorkflows    `

  - **Method** : `  google.cloud.bigquery.migration.v2.MigrationService.ListMigrationWorkflows  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  bigquerymigration.workflows.list - DATA_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.migration.v2.MigrationService.ListMigrationWorkflows"  `  

#### `     StartMigrationWorkflow    `

  - **Method** : `  google.cloud.bigquery.migration.v2.MigrationService.StartMigrationWorkflow  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  bigquerymigration.workflows.update - DATA_WRITE  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.migration.v2.MigrationService.StartMigrationWorkflow"  `  

### `     google.cloud.bigquery.migration.v2.SqlTranslationService    `

The following audit logs are associated with methods belonging to `  google.cloud.bigquery.migration.v2.SqlTranslationService  ` .

#### `     TranslateQuery    `

  - **Method** : `  google.cloud.bigquery.migration.v2.SqlTranslationService.TranslateQuery  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  bigquerymigration.translation.translate - DATA_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.migration.v2.SqlTranslationService.TranslateQuery"  `  

### `     google.cloud.bigquery.migration.v2alpha.MigrationService    `

The following audit logs are associated with methods belonging to `  google.cloud.bigquery.migration.v2alpha.MigrationService  ` .

#### `     CreateMigrationWorkflow    `

  - **Method** : `  google.cloud.bigquery.migration.v2alpha.MigrationService.CreateMigrationWorkflow  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  bigquerymigration.workflows.create - DATA_WRITE  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.migration.v2alpha.MigrationService.CreateMigrationWorkflow"  `  

#### `     DeleteMigrationWorkflow    `

  - **Method** : `  google.cloud.bigquery.migration.v2alpha.MigrationService.DeleteMigrationWorkflow  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  bigquerymigration.workflows.delete - DATA_WRITE  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.migration.v2alpha.MigrationService.DeleteMigrationWorkflow"  `  

#### `     GetMigrationSubtask    `

  - **Method** : `  google.cloud.bigquery.migration.v2alpha.MigrationService.GetMigrationSubtask  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  bigquerymigration.subtasks.get - DATA_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.migration.v2alpha.MigrationService.GetMigrationSubtask"  `  

#### `     GetMigrationWorkflow    `

  - **Method** : `  google.cloud.bigquery.migration.v2alpha.MigrationService.GetMigrationWorkflow  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  bigquerymigration.workflows.get - DATA_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.migration.v2alpha.MigrationService.GetMigrationWorkflow"  `  

#### `     ListMigrationSubtasks    `

  - **Method** : `  google.cloud.bigquery.migration.v2alpha.MigrationService.ListMigrationSubtasks  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  bigquerymigration.subtasks.list - DATA_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.migration.v2alpha.MigrationService.ListMigrationSubtasks"  `  

#### `     ListMigrationWorkflows    `

  - **Method** : `  google.cloud.bigquery.migration.v2alpha.MigrationService.ListMigrationWorkflows  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  bigquerymigration.workflows.list - DATA_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.migration.v2alpha.MigrationService.ListMigrationWorkflows"  `  

#### `     StartMigrationWorkflow    `

  - **Method** : `  google.cloud.bigquery.migration.v2alpha.MigrationService.StartMigrationWorkflow  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  bigquerymigration.workflows.update - DATA_WRITE  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.migration.v2alpha.MigrationService.StartMigrationWorkflow"  `  

### `     google.cloud.bigquery.migration.v2alpha.SqlTranslationService    `

The following audit logs are associated with methods belonging to `  google.cloud.bigquery.migration.v2alpha.SqlTranslationService  ` .

#### `     TranslateQuery    `

  - **Method** : `  google.cloud.bigquery.migration.v2alpha.SqlTranslationService.TranslateQuery  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  bigquerymigration.translation.translate - DATA_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.migration.v2alpha.SqlTranslationService.TranslateQuery"  `
