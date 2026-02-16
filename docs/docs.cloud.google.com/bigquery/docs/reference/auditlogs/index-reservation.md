# BigQuery Reservation API audit logging

This document describes audit logging for BigQuery Reservation API. Google Cloud services generate audit logs that record administrative and access activities within your Google Cloud resources. For more information about Cloud Audit Logs, see the following:

  - [Types of audit logs](/logging/docs/audit#types)
  - [Audit log entry structure](/logging/docs/audit#audit_log_entry_structure)
  - [Storing and routing audit logs](/logging/docs/audit#storing_and_routing_audit_logs)
  - [Cloud Logging pricing summary](/stackdriver/pricing#logs-pricing-summary)
  - [Enable Data Access audit logs](/logging/docs/audit/configure-data-access)

## Service name

BigQuery Reservation API audit logs use the service name `  bigqueryreservation.googleapis.com  ` . Filter for this service:

``` text
    protoPayload.serviceName="bigqueryreservation.googleapis.com"
  
```

## Methods by permission type

Each IAM permission has a `  type  ` property, whose value is an enum that can be one of four values: `  ADMIN_READ  ` , `  ADMIN_WRITE  ` , `  DATA_READ  ` , or `  DATA_WRITE  ` . When you call a method, BigQuery Reservation API generates an audit log whose category is dependent on the `  type  ` property of the permission required to perform the method. Methods that require an IAM permission with the `  type  ` property value of `  DATA_READ  ` , `  DATA_WRITE  ` , or `  ADMIN_READ  ` generate [Data Access](/logging/docs/audit#data-access) audit logs. Methods that require an IAM permission with the `  type  ` property value of `  ADMIN_WRITE  ` generate [Admin Activity](/logging/docs/audit#admin-activity) audit logs.

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
<td><code dir="ltr" translate="no">       google.cloud.bigquery.reservation.v1.ReservationService.GetBiReservation      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.reservation.v1.ReservationService.GetCapacityCommitment      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.reservation.v1.ReservationService.GetReservation      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.reservation.v1.ReservationService.ListAssignments      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.reservation.v1.ReservationService.ListCapacityCommitments      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.reservation.v1.ReservationService.ListReservations      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.reservation.v1.ReservationService.SearchAllAssignments      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.reservation.v1.ReservationService.SearchAssignments      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       ADMIN_WRITE      </code></td>
<td><code dir="ltr" translate="no">       google.cloud.bigquery.reservation.v1.ReservationService.CreateAssignment      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.reservation.v1.ReservationService.CreateCapacityCommitment      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.reservation.v1.ReservationService.CreateReservation      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.reservation.v1.ReservationService.DeleteAssignment      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.reservation.v1.ReservationService.DeleteCapacityCommitment      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.reservation.v1.ReservationService.DeleteReservation      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.reservation.v1.ReservationService.FailoverReservation      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.reservation.v1.ReservationService.MergeCapacityCommitments      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.reservation.v1.ReservationService.MoveAssignment      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.reservation.v1.ReservationService.SplitCapacityCommitment      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.reservation.v1.ReservationService.UpdateAssignment      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.reservation.v1.ReservationService.UpdateBiReservation      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.reservation.v1.ReservationService.UpdateCapacityCommitment      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.reservation.v1.ReservationService.UpdateReservation      </code></td>
</tr>
</tbody>
</table>

## API interface audit logs

For information about how and which permissions are evaluated for each method, see the [Identity and Access Management documentation](/bigquery/docs/reservations-tasks) for BigQuery Reservation API.

### `     google.cloud.bigquery.reservation.v1.ReservationService    `

The following audit logs are associated with methods belonging to `  google.cloud.bigquery.reservation.v1.ReservationService  ` .

#### `     CreateAssignment    `

  - **Method** : `  google.cloud.bigquery.reservation.v1.ReservationService.CreateAssignment  `  
  - **Audit log type** : [Admin activity](/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `  bigquery.reservationAssignments.create - ADMIN_WRITE  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.reservation.v1.ReservationService.CreateAssignment"  `  

#### `     CreateCapacityCommitment    `

  - **Method** : `  google.cloud.bigquery.reservation.v1.ReservationService.CreateCapacityCommitment  `  
  - **Audit log type** : [Admin activity](/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `  bigquery.capacityCommitments.create - ADMIN_WRITE  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.reservation.v1.ReservationService.CreateCapacityCommitment"  `  

#### `     CreateReservation    `

  - **Method** : `  google.cloud.bigquery.reservation.v1.ReservationService.CreateReservation  `  
  - **Audit log type** : [Admin activity](/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `  bigquery.reservations.create - ADMIN_WRITE  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.reservation.v1.ReservationService.CreateReservation"  `  

#### `     DeleteAssignment    `

  - **Method** : `  google.cloud.bigquery.reservation.v1.ReservationService.DeleteAssignment  `  
  - **Audit log type** : [Admin activity](/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `  bigquery.reservationAssignments.delete - ADMIN_WRITE  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.reservation.v1.ReservationService.DeleteAssignment"  `  

#### `     DeleteCapacityCommitment    `

  - **Method** : `  google.cloud.bigquery.reservation.v1.ReservationService.DeleteCapacityCommitment  `  
  - **Audit log type** : [Admin activity](/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `  bigquery.capacityCommitments.delete - ADMIN_WRITE  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.reservation.v1.ReservationService.DeleteCapacityCommitment"  `  

#### `     DeleteReservation    `

  - **Method** : `  google.cloud.bigquery.reservation.v1.ReservationService.DeleteReservation  `  
  - **Audit log type** : [Admin activity](/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `  bigquery.reservations.delete - ADMIN_WRITE  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.reservation.v1.ReservationService.DeleteReservation"  `  

#### `     FailoverReservation    `

  - **Method** : `  google.cloud.bigquery.reservation.v1.ReservationService.FailoverReservation  `  
  - **Audit log type** : [Admin activity](/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `  bigquery.reservations.update - ADMIN_WRITE  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.reservation.v1.ReservationService.FailoverReservation"  `  

#### `     GetBiReservation    `

  - **Method** : `  google.cloud.bigquery.reservation.v1.ReservationService.GetBiReservation  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  bigquery.bireservations.get - ADMIN_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.reservation.v1.ReservationService.GetBiReservation"  `  

#### `     GetCapacityCommitment    `

  - **Method** : `  google.cloud.bigquery.reservation.v1.ReservationService.GetCapacityCommitment  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  bigquery.capacityCommitments.get - ADMIN_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.reservation.v1.ReservationService.GetCapacityCommitment"  `  

#### `     GetReservation    `

  - **Method** : `  google.cloud.bigquery.reservation.v1.ReservationService.GetReservation  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  bigquery.reservations.get - ADMIN_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.reservation.v1.ReservationService.GetReservation"  `  

#### `     ListAssignments    `

  - **Method** : `  google.cloud.bigquery.reservation.v1.ReservationService.ListAssignments  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  bigquery.reservationAssignments.list - ADMIN_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.reservation.v1.ReservationService.ListAssignments"  `  

#### `     ListCapacityCommitments    `

  - **Method** : `  google.cloud.bigquery.reservation.v1.ReservationService.ListCapacityCommitments  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  bigquery.capacityCommitments.list - ADMIN_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.reservation.v1.ReservationService.ListCapacityCommitments"  `  

#### `     ListReservations    `

  - **Method** : `  google.cloud.bigquery.reservation.v1.ReservationService.ListReservations  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  bigquery.reservations.list - ADMIN_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.reservation.v1.ReservationService.ListReservations"  `  

#### `     MergeCapacityCommitments    `

  - **Method** : `  google.cloud.bigquery.reservation.v1.ReservationService.MergeCapacityCommitments  `  
  - **Audit log type** : [Admin activity](/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `  bigquery.capacityCommitments.update - ADMIN_WRITE  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.reservation.v1.ReservationService.MergeCapacityCommitments"  `  

#### `     MoveAssignment    `

  - **Method** : `  google.cloud.bigquery.reservation.v1.ReservationService.MoveAssignment  `  
  - **Audit log type** : [Admin activity](/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `  bigquery.reservationAssignments.create - ADMIN_WRITE  `
      - `  bigquery.reservationAssignments.delete - ADMIN_WRITE  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.reservation.v1.ReservationService.MoveAssignment"  `  

#### `     SearchAllAssignments    `

  - **Method** : `  google.cloud.bigquery.reservation.v1.ReservationService.SearchAllAssignments  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  bigquery.reservationAssignments.search - ADMIN_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.reservation.v1.ReservationService.SearchAllAssignments"  `  

#### `     SearchAssignments    `

  - **Method** : `  google.cloud.bigquery.reservation.v1.ReservationService.SearchAssignments  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  bigquery.reservationAssignments.search - ADMIN_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.reservation.v1.ReservationService.SearchAssignments"  `  

#### `     SplitCapacityCommitment    `

  - **Method** : `  google.cloud.bigquery.reservation.v1.ReservationService.SplitCapacityCommitment  `  
  - **Audit log type** : [Admin activity](/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `  bigquery.capacityCommitments.update - ADMIN_WRITE  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.reservation.v1.ReservationService.SplitCapacityCommitment"  `  

#### `     UpdateAssignment    `

  - **Method** : `  google.cloud.bigquery.reservation.v1.ReservationService.UpdateAssignment  `  
  - **Audit log type** : [Admin activity](/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `  bigquery.reservationAssignments.update - ADMIN_WRITE  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.reservation.v1.ReservationService.UpdateAssignment"  `  

#### `     UpdateBiReservation    `

  - **Method** : `  google.cloud.bigquery.reservation.v1.ReservationService.UpdateBiReservation  `  
  - **Audit log type** : [Admin activity](/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `  bigquery.bireservations.update - ADMIN_WRITE  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.reservation.v1.ReservationService.UpdateBiReservation"  `  

#### `     UpdateCapacityCommitment    `

  - **Method** : `  google.cloud.bigquery.reservation.v1.ReservationService.UpdateCapacityCommitment  `  
  - **Audit log type** : [Admin activity](/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `  bigquery.capacityCommitments.update - ADMIN_WRITE  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.reservation.v1.ReservationService.UpdateCapacityCommitment"  `  

#### `     UpdateReservation    `

  - **Method** : `  google.cloud.bigquery.reservation.v1.ReservationService.UpdateReservation  `  
  - **Audit log type** : [Admin activity](/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `  bigquery.reservations.update - ADMIN_WRITE  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.reservation.v1.ReservationService.UpdateReservation"  `  

## Audit Log examples for BigQuery Reservations usage

The following examples use [`  AuditLog  `](/logging/docs/reference/audit/auditlog/rest/Shared.Types/AuditLog) messages to analyze [BigQuery Reservations](/bigquery/docs/reservations-intro) usage.

### Example: Find users who purchased slots

This query shows the email address of the users who purchased slots.

``` text
  #standardSQL
  SELECT
    protopayload_auditlog.requestMetadata.requestAttributes.time request_time,
    protopayload_auditlog.methodName,
    protopayload_auditlog.authenticationInfo.principalEmail,
    JSON_QUERY(protopayload_auditlog.requestJson , "$.capacityCommitment.slotCount") slots,
  FROM
    `my-project-id.auditlog_dataset.cloudaudit_googleapis_com_activity`
  WHERE
    protopayload_auditlog.methodName like "%CreateCapacityCommitment%"
  ORDER by request_time
```

### Example: History of a project assignment

This query shows the history of a project's reservation assignments.

``` text
  #standardSQL
  SELECT
    protopayload_auditlog.requestMetadata.requestAttributes.time request_time,
    protopayload_auditlog.methodName,
    protopayload_auditlog.authenticationInfo.principalEmail,
    JSON_QUERY(protopayload_auditlog.requestJson , "$.assignment.assignee") assignee,
    JSON_QUERY(protopayload_auditlog.requestJson , "$.assignment.jobType") job_type,
  FROM
    `my-project-id.auditlog_dataset.cloudaudit_googleapis_com_activity`
  WHERE
    protopayload_auditlog.methodName like "%Assignment%"
    AND JSON_QUERY(protopayload_auditlog.requestJson , "$.assignment.assignee") like "%OTHERPROJECTID%"
  ORDER by request_time
```
