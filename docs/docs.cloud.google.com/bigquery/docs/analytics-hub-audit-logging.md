# Sharing audit logging

This document describes audit logging for BigQuery sharing. Google Cloud services generate audit logs that record administrative and access activities within your Google Cloud resources. For more information about Cloud Audit Logs, see the following:

  - [Types of audit logs](/logging/docs/audit#types)
  - [Audit log entry structure](/logging/docs/audit#audit_log_entry_structure)
  - [Storing and routing audit logs](/logging/docs/audit#storing_and_routing_audit_logs)
  - [Cloud Logging pricing summary](/stackdriver/pricing#logs-pricing-summary)
  - [Enable Data Access audit logs](/logging/docs/audit/configure-data-access)

## Service name

BigQuery sharing audit logs use the service name `  analyticshub.googleapis.com  ` . Filter for this service:

``` text
    protoPayload.serviceName="analyticshub.googleapis.com"
  
```

## Methods by permission type

Each IAM permission has a `  type  ` property, whose value is an enum that can be one of four values: `  ADMIN_READ  ` , `  ADMIN_WRITE  ` , `  DATA_READ  ` , or `  DATA_WRITE  ` . When you call a method, BigQuery sharing generates an audit log whose category is dependent on the `  type  ` property of the permission required to perform the method. Methods that require an IAM permission with the `  type  ` property value of `  DATA_READ  ` , `  DATA_WRITE  ` , or `  ADMIN_READ  ` generate [Data Access](/logging/docs/audit#data-access) audit logs. Methods that require an IAM permission with the `  type  ` property value of `  ADMIN_WRITE  ` generate [Admin Activity](/logging/docs/audit#admin-activity) audit logs.

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
<td><code dir="ltr" translate="no">       google.cloud.bigquery.analyticshub.v1.AnalyticsHubService.GetDataExchange      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.analyticshub.v1.AnalyticsHubService.GetIamPolicy      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.analyticshub.v1.AnalyticsHubService.GetListing      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.analyticshub.v1.AnalyticsHubService.GetSubscription      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.analyticshub.v1.AnalyticsHubService.ListDataExchanges      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.analyticshub.v1.AnalyticsHubService.ListListings      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.analyticshub.v1.AnalyticsHubService.ListOrgDataExchanges      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.analyticshub.v1.AnalyticsHubService.ListSharedResourceSubscriptions      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.analyticshub.v1.AnalyticsHubService.ListSubscriptions      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.dataexchange.v1beta1.AnalyticsHubService.GetDataExchange      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.dataexchange.v1beta1.AnalyticsHubService.GetIamPolicy      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.dataexchange.v1beta1.AnalyticsHubService.GetListing      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.dataexchange.v1beta1.AnalyticsHubService.ListDataExchanges      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.dataexchange.v1beta1.AnalyticsHubService.ListListings      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.dataexchange.v1beta1.AnalyticsHubService.ListOrgDataExchanges      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.dataexchange.v1beta1.AnalyticsHubService.SubscribeListing      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       ADMIN_WRITE      </code></td>
<td><code dir="ltr" translate="no">       google.cloud.bigquery.analyticshub.v1.AnalyticsHubService.CreateDataExchange      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.analyticshub.v1.AnalyticsHubService.CreateListing      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.analyticshub.v1.AnalyticsHubService.DeleteDataExchange      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.analyticshub.v1.AnalyticsHubService.DeleteListing      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.analyticshub.v1.AnalyticsHubService.DeleteSubscription      </code> (LRO)<br />
<code dir="ltr" translate="no">       google.cloud.bigquery.analyticshub.v1.AnalyticsHubService.RefreshSubscription      </code> (LRO)<br />
<code dir="ltr" translate="no">       google.cloud.bigquery.analyticshub.v1.AnalyticsHubService.RevokeSubscription      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.analyticshub.v1.AnalyticsHubService.SetIamPolicy      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.analyticshub.v1.AnalyticsHubService.SubscribeDataExchange      </code> (LRO)<br />
<code dir="ltr" translate="no">       google.cloud.bigquery.analyticshub.v1.AnalyticsHubService.SubscribeListing      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.analyticshub.v1.AnalyticsHubService.UpdateDataExchange      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.analyticshub.v1.AnalyticsHubService.UpdateListing      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.dataexchange.v1beta1.AnalyticsHubService.CreateDataExchange      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.dataexchange.v1beta1.AnalyticsHubService.CreateListing      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.dataexchange.v1beta1.AnalyticsHubService.DeleteDataExchange      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.dataexchange.v1beta1.AnalyticsHubService.DeleteListing      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.dataexchange.v1beta1.AnalyticsHubService.SetIamPolicy      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.dataexchange.v1beta1.AnalyticsHubService.UpdateDataExchange      </code><br />
<code dir="ltr" translate="no">       google.cloud.bigquery.dataexchange.v1beta1.AnalyticsHubService.UpdateListing      </code></td>
</tr>
</tbody>
</table>

## API interface audit logs

For information about how and which permissions are evaluated for each method, see the Identity and Access Management documentation for BigQuery sharing.

### `     google.cloud.bigquery.analyticshub.v1.AnalyticsHubService    `

The following audit logs are associated with methods belonging to `  google.cloud.bigquery.analyticshub.v1.AnalyticsHubService  ` .

#### `     CreateDataExchange    `

  - **Method** : `  google.cloud.bigquery.analyticshub.v1.AnalyticsHubService.CreateDataExchange  `  
  - **Audit log type** : [Admin activity](/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `  analyticshub.dataExchanges.create - ADMIN_WRITE  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.analyticshub.v1.AnalyticsHubService.CreateDataExchange"  `  

#### `     CreateListing    `

  - **Method** : `  google.cloud.bigquery.analyticshub.v1.AnalyticsHubService.CreateListing  `  
  - **Audit log type** : [Admin activity](/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `  analyticshub.listings.create - ADMIN_WRITE  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.analyticshub.v1.AnalyticsHubService.CreateListing"  `  

#### `     DeleteDataExchange    `

  - **Method** : `  google.cloud.bigquery.analyticshub.v1.AnalyticsHubService.DeleteDataExchange  `  
  - **Audit log type** : [Admin activity](/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `  analyticshub.dataExchanges.delete - ADMIN_WRITE  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.analyticshub.v1.AnalyticsHubService.DeleteDataExchange"  `  

#### `     DeleteListing    `

  - **Method** : `  google.cloud.bigquery.analyticshub.v1.AnalyticsHubService.DeleteListing  `  
  - **Audit log type** : [Admin activity](/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `  analyticshub.listings.delete - ADMIN_WRITE  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.analyticshub.v1.AnalyticsHubService.DeleteListing"  `  

#### `     DeleteSubscription    `

  - **Method** : `  google.cloud.bigquery.analyticshub.v1.AnalyticsHubService.DeleteSubscription  `  
  - **Audit log type** : [Admin activity](/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `  analyticshub.subscriptions.delete - ADMIN_WRITE  `
  - **Method is a long-running or streaming operation** : [**Long-running operation**](/logging/docs/audit/understanding-audit-logs#lro)  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.analyticshub.v1.AnalyticsHubService.DeleteSubscription"  `  

#### `     GetDataExchange    `

  - **Method** : `  google.cloud.bigquery.analyticshub.v1.AnalyticsHubService.GetDataExchange  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  analyticshub.dataExchanges.get - ADMIN_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.analyticshub.v1.AnalyticsHubService.GetDataExchange"  `  

#### `     GetIamPolicy    `

  - **Method** : `  google.cloud.bigquery.analyticshub.v1.AnalyticsHubService.GetIamPolicy  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  analyticshub.dataExchanges.getIamPolicy - ADMIN_READ  `
      - `  analyticshub.listings.getIamPolicy - ADMIN_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.analyticshub.v1.AnalyticsHubService.GetIamPolicy"  `  

#### `     GetListing    `

  - **Method** : `  google.cloud.bigquery.analyticshub.v1.AnalyticsHubService.GetListing  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  analyticshub.listings.get - ADMIN_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.analyticshub.v1.AnalyticsHubService.GetListing"  `  

#### `     GetSubscription    `

  - **Method** : `  google.cloud.bigquery.analyticshub.v1.AnalyticsHubService.GetSubscription  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  analyticshub.subscriptions.get - ADMIN_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.analyticshub.v1.AnalyticsHubService.GetSubscription"  `  

#### `     ListDataExchanges    `

  - **Method** : `  google.cloud.bigquery.analyticshub.v1.AnalyticsHubService.ListDataExchanges  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  analyticshub.dataExchanges.list - ADMIN_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.analyticshub.v1.AnalyticsHubService.ListDataExchanges"  `  

#### `     ListListings    `

  - **Method** : `  google.cloud.bigquery.analyticshub.v1.AnalyticsHubService.ListListings  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  analyticshub.listings.list - ADMIN_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.analyticshub.v1.AnalyticsHubService.ListListings"  `  

#### `     ListOrgDataExchanges    `

  - **Method** : `  google.cloud.bigquery.analyticshub.v1.AnalyticsHubService.ListOrgDataExchanges  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  analyticshub.dataExchanges.get - ADMIN_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.analyticshub.v1.AnalyticsHubService.ListOrgDataExchanges"  `  

#### `     ListSharedResourceSubscriptions    `

  - **Method** : `  google.cloud.bigquery.analyticshub.v1.AnalyticsHubService.ListSharedResourceSubscriptions  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  analyticshub.listings.viewSubscriptions - ADMIN_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.analyticshub.v1.AnalyticsHubService.ListSharedResourceSubscriptions"  `  

#### `     ListSubscriptions    `

  - **Method** : `  google.cloud.bigquery.analyticshub.v1.AnalyticsHubService.ListSubscriptions  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  analyticshub.subscriptions.list - ADMIN_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.analyticshub.v1.AnalyticsHubService.ListSubscriptions"  `  

#### `     RefreshSubscription    `

  - **Method** : `  google.cloud.bigquery.analyticshub.v1.AnalyticsHubService.RefreshSubscription  `  
  - **Audit log type** : [Admin activity](/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `  analyticshub.subscriptions.update - ADMIN_WRITE  `
  - **Method is a long-running or streaming operation** : [**Long-running operation**](/logging/docs/audit/understanding-audit-logs#lro)  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.analyticshub.v1.AnalyticsHubService.RefreshSubscription"  `  

#### `     RevokeSubscription    `

  - **Method** : `  google.cloud.bigquery.analyticshub.v1.AnalyticsHubService.RevokeSubscription  `  
  - **Audit log type** : [Admin activity](/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `  analyticshub.dataExchanges.update - ADMIN_WRITE  `
      - `  analyticshub.listings.update - ADMIN_WRITE  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.analyticshub.v1.AnalyticsHubService.RevokeSubscription"  `  

#### `     SetIamPolicy    `

  - **Method** : `  google.cloud.bigquery.analyticshub.v1.AnalyticsHubService.SetIamPolicy  `  
  - **Audit log type** : [Admin activity](/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `  analyticshub.listings.setIamPolicy - ADMIN_WRITE  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.analyticshub.v1.AnalyticsHubService.SetIamPolicy"  `  

#### `     SubscribeDataExchange    `

  - **Method** : `  google.cloud.bigquery.analyticshub.v1.AnalyticsHubService.SubscribeDataExchange  `  
  - **Audit log type** : [Admin activity](/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `  analyticshub.subscriptions.create - ADMIN_WRITE  `
  - **Method is a long-running or streaming operation** : [**Long-running operation**](/logging/docs/audit/understanding-audit-logs#lro)  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.analyticshub.v1.AnalyticsHubService.SubscribeDataExchange"  `  

#### `     SubscribeListing    `

  - **Method** : `  google.cloud.bigquery.analyticshub.v1.AnalyticsHubService.SubscribeListing  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  analyticshub.listings.subscribe - ADMIN_WRITE  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.analyticshub.v1.AnalyticsHubService.SubscribeListing"  `  

#### `     UpdateDataExchange    `

  - **Method** : `  google.cloud.bigquery.analyticshub.v1.AnalyticsHubService.UpdateDataExchange  `  
  - **Audit log type** : [Admin activity](/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `  analyticshub.dataExchanges.update - ADMIN_WRITE  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.analyticshub.v1.AnalyticsHubService.UpdateDataExchange"  `  

#### `     UpdateListing    `

  - **Method** : `  google.cloud.bigquery.analyticshub.v1.AnalyticsHubService.UpdateListing  `  
  - **Audit log type** : [Admin activity](/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `  analyticshub.listings.update - ADMIN_WRITE  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.analyticshub.v1.AnalyticsHubService.UpdateListing"  `  

### `     google.cloud.bigquery.dataexchange.v1beta1.AnalyticsHubService    `

The following audit logs are associated with methods belonging to `  google.cloud.bigquery.dataexchange.v1beta1.AnalyticsHubService  ` .

#### `     CreateDataExchange    `

  - **Method** : `  google.cloud.bigquery.dataexchange.v1beta1.AnalyticsHubService.CreateDataExchange  `  
  - **Audit log type** : [Admin activity](/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `  analyticshub.dataExchanges.create - ADMIN_WRITE  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.dataexchange.v1beta1.AnalyticsHubService.CreateDataExchange"  `  

#### `     CreateListing    `

  - **Method** : `  google.cloud.bigquery.dataexchange.v1beta1.AnalyticsHubService.CreateListing  `  
  - **Audit log type** : [Admin activity](/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `  analyticshub.listings.create - ADMIN_WRITE  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.dataexchange.v1beta1.AnalyticsHubService.CreateListing"  `  

#### `     DeleteDataExchange    `

  - **Method** : `  google.cloud.bigquery.dataexchange.v1beta1.AnalyticsHubService.DeleteDataExchange  `  
  - **Audit log type** : [Admin activity](/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `  analyticshub.dataExchanges.delete - ADMIN_WRITE  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.dataexchange.v1beta1.AnalyticsHubService.DeleteDataExchange"  `  

#### `     DeleteListing    `

  - **Method** : `  google.cloud.bigquery.dataexchange.v1beta1.AnalyticsHubService.DeleteListing  `  
  - **Audit log type** : [Admin activity](/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `  analyticshub.listings.delete - ADMIN_WRITE  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.dataexchange.v1beta1.AnalyticsHubService.DeleteListing"  `  

#### `     GetDataExchange    `

  - **Method** : `  google.cloud.bigquery.dataexchange.v1beta1.AnalyticsHubService.GetDataExchange  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  analyticshub.dataExchanges.get - ADMIN_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.dataexchange.v1beta1.AnalyticsHubService.GetDataExchange"  `  

#### `     GetIamPolicy    `

  - **Method** : `  google.cloud.bigquery.dataexchange.v1beta1.AnalyticsHubService.GetIamPolicy  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  analyticshub.dataExchanges.getIamPolicy - ADMIN_READ  `
      - `  analyticshub.listings.getIamPolicy - ADMIN_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.dataexchange.v1beta1.AnalyticsHubService.GetIamPolicy"  `  

#### `     GetListing    `

  - **Method** : `  google.cloud.bigquery.dataexchange.v1beta1.AnalyticsHubService.GetListing  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  analyticshub.listings.get - ADMIN_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.dataexchange.v1beta1.AnalyticsHubService.GetListing"  `  

#### `     ListDataExchanges    `

  - **Method** : `  google.cloud.bigquery.dataexchange.v1beta1.AnalyticsHubService.ListDataExchanges  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  analyticshub.dataExchanges.list - ADMIN_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.dataexchange.v1beta1.AnalyticsHubService.ListDataExchanges"  `  

#### `     ListListings    `

  - **Method** : `  google.cloud.bigquery.dataexchange.v1beta1.AnalyticsHubService.ListListings  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  analyticshub.listings.list - ADMIN_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.dataexchange.v1beta1.AnalyticsHubService.ListListings"  `  

#### `     ListOrgDataExchanges    `

  - **Method** : `  google.cloud.bigquery.dataexchange.v1beta1.AnalyticsHubService.ListOrgDataExchanges  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  analyticshub.dataExchanges.get - ADMIN_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.dataexchange.v1beta1.AnalyticsHubService.ListOrgDataExchanges"  `  

#### `     SetIamPolicy    `

  - **Method** : `  google.cloud.bigquery.dataexchange.v1beta1.AnalyticsHubService.SetIamPolicy  `  
  - **Audit log type** : [Admin activity](/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `  analyticshub.listings.setIamPolicy - ADMIN_WRITE  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.dataexchange.v1beta1.AnalyticsHubService.SetIamPolicy"  `  

#### `     SubscribeListing    `

  - **Method** : `  google.cloud.bigquery.dataexchange.v1beta1.AnalyticsHubService.SubscribeListing  `  
  - **Audit log type** : [Data access](/logging/docs/audit#data-access)  
  - **Permissions** :
      - `  analyticshub.listings.subscribe - ADMIN_READ  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.dataexchange.v1beta1.AnalyticsHubService.SubscribeListing"  `  

#### `     UpdateDataExchange    `

  - **Method** : `  google.cloud.bigquery.dataexchange.v1beta1.AnalyticsHubService.UpdateDataExchange  `  
  - **Audit log type** : [Admin activity](/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `  analyticshub.dataExchanges.update - ADMIN_WRITE  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.dataexchange.v1beta1.AnalyticsHubService.UpdateDataExchange"  `  

#### `     UpdateListing    `

  - **Method** : `  google.cloud.bigquery.dataexchange.v1beta1.AnalyticsHubService.UpdateListing  `  
  - **Audit log type** : [Admin activity](/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `  analyticshub.listings.update - ADMIN_WRITE  `
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `  protoPayload.methodName="google.cloud.bigquery.dataexchange.v1beta1.AnalyticsHubService.UpdateListing"  `  

## Methods that don't produce audit logs

A method might not produce audit logs for one or more of the following reasons:

  - It is a high volume method involving significant log generation and storage costs.
  - It has low auditing value.
  - Another audit or platform log already provides method coverage.

The following methods don't produce audit logs:

  - `  google.cloud.bigquery.analyticshub.v1.AnalyticsHubService.TestIamPermissions  `
  - `  google.cloud.bigquery.dataexchange.v1beta1.AnalyticsHubService.TestIamPermissions  `
