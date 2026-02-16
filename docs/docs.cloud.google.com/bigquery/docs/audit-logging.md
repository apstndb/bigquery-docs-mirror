# BigQuery Data Transfer Service audit logging

This document describes audit logging for BigQuery Data Transfer Service. Google Cloud services generate audit logs that record administrative and access activities within your Google Cloud resources. For more information about Cloud Audit Logs, see the following:

  - [Types of audit logs](/logging/docs/audit#types)
  - [Audit log entry structure](/logging/docs/audit#audit_log_entry_structure)
  - [Storing and routing audit logs](/logging/docs/audit#storing_and_routing_audit_logs)
  - [Cloud Logging pricing summary](/stackdriver/pricing#logs-pricing-summary)
  - [Enable Data Access audit logs](/logging/docs/audit/configure-data-access)

## Service name

BigQuery Data Transfer Service audit logs use the service name `  bigquerydatatransfer.googleapis.com  ` . Filter for this service:

``` text
    protoPayload.serviceName="bigquerydatatransfer.googleapis.com"
  
```

## Methods by permission type

Each IAM permission has a `  type  ` property, whose value is an enum that can be one of four values: `  ADMIN_READ  ` , `  ADMIN_WRITE  ` , `  DATA_READ  ` , or `  DATA_WRITE  ` . When you call a method, BigQuery Data Transfer Service generates an audit log whose category is dependent on the `  type  ` property of the permission required to perform the method. Methods that require an IAM permission with the `  type  ` property value of `  DATA_READ  ` , `  DATA_WRITE  ` , or `  ADMIN_READ  ` generate [Data Access](/logging/docs/audit#data-access) audit logs. Methods that require an IAM permission with the `  type  ` property value of `  ADMIN_WRITE  ` generate [Admin Activity](/logging/docs/audit#admin-activity) audit logs.

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
<td><code dir="ltr" translate="no">       google.cloud.bigquery.datatransfer.v1.DataTransferService.CheckValidCreds      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.datatransfer.v1.DataTransferService.GetDataSource      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.datatransfer.v1.DataTransferService.GetTransferConfig      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.datatransfer.v1.DataTransferService.GetTransferRun      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.datatransfer.v1.DataTransferService.ListDataSources      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.datatransfer.v1.DataTransferService.ListTransferConfigs      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.datatransfer.v1.DataTransferService.ListTransferLogs      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.datatransfer.v1.DataTransferService.ListTransferRuns      </code><br />
<code dir="ltr" translate="no">       google.cloud.location.Locations.GetLocation      </code><br />
<code dir="ltr" translate="no">       google.cloud.location.Locations.ListLocations      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       ADMIN_WRITE      </code></td>
<td><code dir="ltr" translate="no">       google.cloud.bigquery.datatransfer.v1.DataTransferService.CreateTransferConfig      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.datatransfer.v1.DataTransferService.DeleteTransferConfig      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.datatransfer.v1.DataTransferService.DeleteTransferRun      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.datatransfer.v1.DataTransferService.EnrollDataSources      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.datatransfer.v1.DataTransferService.ScheduleTransferRuns      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.datatransfer.v1.DataTransferService.StartManualTransferRuns      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.datatransfer.v1.DataTransferService.UnenrollDataSources      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.datatransfer.v1.DataTransferService.UpdateTransferConfig      </code></td>
</tr>
</tbody>
</table>

## API interface audit logs

For information about how and which permissions are evaluated for each method, see the Identity and Access Management documentation for BigQuery Data Transfer Service.

### `     google.cloud.bigquery.datatransfer.v1.DataTransferService    `

The following audit logs are associated with methods belonging to `  google.cloud.bigquery.datatransfer.v1.DataTransferService  ` .

#### `     CheckValidCreds    `

  - **Method** : `  google.cloud.bigquery.datatransfer.v1.DataTransferService.CheckValidCreds  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  bigquery.transfers.get - ADMIN_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.datatransfer.v1.DataTransferService.CheckValidCreds"  `  

#### `     CreateTransferConfig    `

  - **Method** : `  google.cloud.bigquery.datatransfer.v1.DataTransferService.CreateTransferConfig  `  
  - **Audit log type** : [Admin activity](/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `  bigquery.transfers.update - ADMIN_WRITE  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.datatransfer.v1.DataTransferService.CreateTransferConfig"  `  

#### `     DeleteTransferConfig    `

  - **Method** : `  google.cloud.bigquery.datatransfer.v1.DataTransferService.DeleteTransferConfig  `  
  - **Audit log type** : [Admin activity](/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `  bigquery.transfers.update - ADMIN_WRITE  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.datatransfer.v1.DataTransferService.DeleteTransferConfig"  `  

#### `     DeleteTransferRun    `

  - **Method** : `  google.cloud.bigquery.datatransfer.v1.DataTransferService.DeleteTransferRun  `  
  - **Audit log type** : [Admin activity](/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `  bigquery.transfers.update - ADMIN_WRITE  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.datatransfer.v1.DataTransferService.DeleteTransferRun"  `  

#### `     EnrollDataSources    `

  - **Method** : `  google.cloud.bigquery.datatransfer.v1.DataTransferService.EnrollDataSources  `  
  - **Audit log type** : [Admin activity](/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `  resourcemanager.projects.update - ADMIN_WRITE  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.datatransfer.v1.DataTransferService.EnrollDataSources"  `  

#### `     GetDataSource    `

  - **Method** : `  google.cloud.bigquery.datatransfer.v1.DataTransferService.GetDataSource  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  bigquery.transfers.get - ADMIN_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.datatransfer.v1.DataTransferService.GetDataSource"  `  

#### `     GetTransferConfig    `

  - **Method** : `  google.cloud.bigquery.datatransfer.v1.DataTransferService.GetTransferConfig  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  bigquery.transfers.get - ADMIN_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.datatransfer.v1.DataTransferService.GetTransferConfig"  `  

#### `     GetTransferRun    `

  - **Method** : `  google.cloud.bigquery.datatransfer.v1.DataTransferService.GetTransferRun  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  bigquery.transfers.get - ADMIN_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.datatransfer.v1.DataTransferService.GetTransferRun"  `  

#### `     ListDataSources    `

  - **Method** : `  google.cloud.bigquery.datatransfer.v1.DataTransferService.ListDataSources  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  bigquery.transfers.get - ADMIN_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.datatransfer.v1.DataTransferService.ListDataSources"  `  

#### `     ListTransferConfigs    `

  - **Method** : `  google.cloud.bigquery.datatransfer.v1.DataTransferService.ListTransferConfigs  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  bigquery.transfers.get - ADMIN_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.datatransfer.v1.DataTransferService.ListTransferConfigs"  `  

#### `     ListTransferLogs    `

  - **Method** : `  google.cloud.bigquery.datatransfer.v1.DataTransferService.ListTransferLogs  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  bigquery.transfers.get - ADMIN_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.datatransfer.v1.DataTransferService.ListTransferLogs"  `  

#### `     ListTransferRuns    `

  - **Method** : `  google.cloud.bigquery.datatransfer.v1.DataTransferService.ListTransferRuns  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  bigquery.transfers.get - ADMIN_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.datatransfer.v1.DataTransferService.ListTransferRuns"  `  

#### `     ScheduleTransferRuns    `

  - **Method** : `  google.cloud.bigquery.datatransfer.v1.DataTransferService.ScheduleTransferRuns  `  
  - **Audit log type** : [Admin activity](/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `  bigquery.transfers.update - ADMIN_WRITE  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.datatransfer.v1.DataTransferService.ScheduleTransferRuns"  `  

#### `     StartManualTransferRuns    `

  - **Method** : `  google.cloud.bigquery.datatransfer.v1.DataTransferService.StartManualTransferRuns  `  
  - **Audit log type** : [Admin activity](/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `  bigquery.transfers.update - ADMIN_WRITE  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.datatransfer.v1.DataTransferService.StartManualTransferRuns"  `  

#### `     UnenrollDataSources    `

  - **Method** : `  google.cloud.bigquery.datatransfer.v1.DataTransferService.UnenrollDataSources  `  
  - **Audit log type** : [Admin activity](/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `  resourcemanager.projects.update - ADMIN_WRITE  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.datatransfer.v1.DataTransferService.UnenrollDataSources"  `  

#### `     UpdateTransferConfig    `

  - **Method** : `  google.cloud.bigquery.datatransfer.v1.DataTransferService.UpdateTransferConfig  `  
  - **Audit log type** : [Admin activity](/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `  bigquery.transfers.update - ADMIN_WRITE  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.datatransfer.v1.DataTransferService.UpdateTransferConfig"  `  

### `     google.cloud.location.Locations    `

The following audit logs are associated with methods belonging to `  google.cloud.location.Locations  ` .

#### `     GetLocation    `

  - **Method** : `  google.cloud.location.Locations.GetLocation  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  bigquery.transfers.get - ADMIN_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.location.Locations.GetLocation"  `  

#### `     ListLocations    `

  - **Method** : `  google.cloud.location.Locations.ListLocations  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  bigquery.transfers.get - ADMIN_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.location.Locations.ListLocations"  `
