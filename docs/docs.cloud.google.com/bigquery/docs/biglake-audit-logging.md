---
name: documents/docs.cloud.google.com/bigquery/docs/biglake-audit-logging
uri: https://docs.cloud.google.com/bigquery/docs/biglake-audit-logging
title: BigLake audit logging
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

# BigLake audit logging

This document lists the audited methods for Lakehouse. Google Cloud services generate audit logs that record administrative and access activities within your Google Cloud resources. For more information about Cloud Audit Logs, see the following:

  - [Types of audit logs](https://docs.cloud.google.com/logging/docs/audit#types)
  - [Audit log entry structure](https://docs.cloud.google.com/logging/docs/audit#audit_log_entry_structure)
  - [Storing and routing audit logs](https://docs.cloud.google.com/logging/docs/audit#storing_and_routing_audit_logs)
  - [Cloud Logging pricing summary](https://docs.cloud.google.com/stackdriver/pricing#logs-pricing-summary)
  - [Enable Data Access audit logs](https://docs.cloud.google.com/logging/docs/audit/configure-data-access)

## Service name

To view the Lakehouse audit logs, do the following:

1.  In the Google Cloud console, go to the Logs Explorer page:

2.  Copy and paste the following query into the **Query** field of the Logs Explorer, and then click **Run query** .
    
    ``` 
        protoPayload.serviceName="biglake.googleapis.com"
      
    ```

## Methods by permission type

Each IAM permission has a `type` property, whose value is an enum that can be one of four values: `ADMIN_READ` , `ADMIN_WRITE` , `DATA_READ` , or `DATA_WRITE` . When you call a method, Lakehouse generates an audit log whose category is dependent on the `type` property of the permission required to perform the method. Methods that require an IAM permission with the `type` property value of `DATA_READ` , `DATA_WRITE` , or `ADMIN_READ` generate [Data Access](https://docs.cloud.google.com/logging/docs/audit#data-access) audit logs. Methods that require an IAM permission with the `type` property value of `ADMIN_WRITE` generate [Admin Activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity) audit logs.

API methods in the following list that are marked with (LRO) are long-running operations (LROs). These methods usually generate two audit log entries: one when the operation starts and another when it ends. For more information see [Audit logs for long-running operations](https://docs.cloud.google.com/logging/docs/audit/understanding-audit-logs#lro) .

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
<td><code dir="ltr" translate="no">ADMIN_READ</code></td>
<td><code dir="ltr" translate="no">google.cloud.biglake.v1.DeltaSharingService.GetDeltaSharingCatalog</code><br />
<code dir="ltr" translate="no">google.cloud.biglake.v1.DeltaSharingService.ListDeltaSharingShares</code><br />
<code dir="ltr" translate="no">google.cloud.biglake.v1.DeltaSharingService.ListDeltaSharingTables</code><br />
<code dir="ltr" translate="no">google.cloud.biglake.v1alpha.DeltaSharingService.GetDeltaSharingCatalog</code><br />
<code dir="ltr" translate="no">google.cloud.bigquery.biglake.v1.MetastoreService.GetCatalog</code><br />
<code dir="ltr" translate="no">google.cloud.bigquery.biglake.v1.MetastoreService.GetDatabase</code><br />
<code dir="ltr" translate="no">google.cloud.bigquery.biglake.v1.MetastoreService.GetTable</code><br />
<code dir="ltr" translate="no">google.cloud.bigquery.biglake.v1.MetastoreService.ListCatalogs</code><br />
<code dir="ltr" translate="no">google.cloud.bigquery.biglake.v1.MetastoreService.ListDatabases</code><br />
<code dir="ltr" translate="no">google.cloud.bigquery.biglake.v1.MetastoreService.ListTables</code><br />
<code dir="ltr" translate="no">google.cloud.bigquery.biglake.v1alpha1.MetastoreService.GetCatalog</code><br />
<code dir="ltr" translate="no">google.cloud.bigquery.biglake.v1alpha1.MetastoreService.GetDatabase</code><br />
<code dir="ltr" translate="no">google.cloud.bigquery.biglake.v1alpha1.MetastoreService.GetTable</code><br />
<code dir="ltr" translate="no">google.cloud.bigquery.biglake.v1alpha1.MetastoreService.ListCatalogs</code><br />
<code dir="ltr" translate="no">google.cloud.bigquery.biglake.v1alpha1.MetastoreService.ListDatabases</code><br />
<code dir="ltr" translate="no">google.cloud.bigquery.biglake.v1alpha1.MetastoreService.ListLocks</code><br />
<code dir="ltr" translate="no">google.cloud.bigquery.biglake.v1alpha1.MetastoreService.ListTables</code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">ADMIN_WRITE</code></td>
<td><code dir="ltr" translate="no">google.cloud.biglake.hive.v1alpha.HiveMetastoreService.BatchCreatePartitions</code><br />
<code dir="ltr" translate="no">google.cloud.biglake.hive.v1alpha.HiveMetastoreService.BatchDeletePartitions</code><br />
<code dir="ltr" translate="no">google.cloud.biglake.hive.v1alpha.HiveMetastoreService.BatchUpdatePartitions</code><br />
<code dir="ltr" translate="no">google.cloud.biglake.hive.v1alpha.HiveMetastoreService.CreateHiveCatalog</code><br />
<code dir="ltr" translate="no">google.cloud.biglake.hive.v1alpha.HiveMetastoreService.CreateHiveDatabase</code><br />
<code dir="ltr" translate="no">google.cloud.biglake.hive.v1alpha.HiveMetastoreService.CreateHiveTable</code><br />
<code dir="ltr" translate="no">google.cloud.biglake.hive.v1alpha.HiveMetastoreService.DeleteHiveCatalog</code><br />
<code dir="ltr" translate="no">google.cloud.biglake.hive.v1alpha.HiveMetastoreService.DeleteHiveDatabase</code><br />
<code dir="ltr" translate="no">google.cloud.biglake.hive.v1alpha.HiveMetastoreService.DeleteHiveTable</code><br />
<code dir="ltr" translate="no">google.cloud.biglake.hive.v1alpha.HiveMetastoreService.GetHiveCatalog</code><br />
<code dir="ltr" translate="no">google.cloud.biglake.hive.v1alpha.HiveMetastoreService.GetHiveDatabase</code><br />
<code dir="ltr" translate="no">google.cloud.biglake.hive.v1alpha.HiveMetastoreService.GetHiveTable</code><br />
<code dir="ltr" translate="no">google.cloud.biglake.hive.v1alpha.HiveMetastoreService.ListHiveDatabases</code><br />
<code dir="ltr" translate="no">google.cloud.biglake.hive.v1alpha.HiveMetastoreService.ListHiveTables</code><br />
<code dir="ltr" translate="no">google.cloud.biglake.hive.v1alpha.HiveMetastoreService.ListPartitions</code><br />
<code dir="ltr" translate="no">google.cloud.biglake.hive.v1alpha.HiveMetastoreService.UpdateHiveCatalog</code><br />
<code dir="ltr" translate="no">google.cloud.biglake.hive.v1alpha.HiveMetastoreService.UpdateHiveDatabase</code><br />
<code dir="ltr" translate="no">google.cloud.biglake.hive.v1alpha.HiveMetastoreService.UpdateHiveTable</code><br />
<code dir="ltr" translate="no">google.cloud.biglake.hive.v1beta.HiveMetastoreService.BatchCreatePartitions</code><br />
<code dir="ltr" translate="no">google.cloud.biglake.hive.v1beta.HiveMetastoreService.BatchDeletePartitions</code><br />
<code dir="ltr" translate="no">google.cloud.biglake.hive.v1beta.HiveMetastoreService.BatchUpdatePartitions</code><br />
<code dir="ltr" translate="no">google.cloud.biglake.hive.v1beta.HiveMetastoreService.CreateHiveCatalog</code><br />
<code dir="ltr" translate="no">google.cloud.biglake.hive.v1beta.HiveMetastoreService.CreateHiveDatabase</code><br />
<code dir="ltr" translate="no">google.cloud.biglake.hive.v1beta.HiveMetastoreService.CreateHiveTable</code><br />
<code dir="ltr" translate="no">google.cloud.biglake.hive.v1beta.HiveMetastoreService.DeleteHiveCatalog</code><br />
<code dir="ltr" translate="no">google.cloud.biglake.hive.v1beta.HiveMetastoreService.DeleteHiveDatabase</code><br />
<code dir="ltr" translate="no">google.cloud.biglake.hive.v1beta.HiveMetastoreService.DeleteHiveTable</code><br />
<code dir="ltr" translate="no">google.cloud.biglake.hive.v1beta.HiveMetastoreService.GetHiveCatalog</code><br />
<code dir="ltr" translate="no">google.cloud.biglake.hive.v1beta.HiveMetastoreService.GetHiveDatabase</code><br />
<code dir="ltr" translate="no">google.cloud.biglake.hive.v1beta.HiveMetastoreService.GetHiveTable</code><br />
<code dir="ltr" translate="no">google.cloud.biglake.hive.v1beta.HiveMetastoreService.ListHiveDatabases</code><br />
<code dir="ltr" translate="no">google.cloud.biglake.hive.v1beta.HiveMetastoreService.ListHiveTables</code><br />
<code dir="ltr" translate="no">google.cloud.biglake.hive.v1beta.HiveMetastoreService.ListPartitions</code><br />
<code dir="ltr" translate="no">google.cloud.biglake.hive.v1beta.HiveMetastoreService.UpdateHiveCatalog</code><br />
<code dir="ltr" translate="no">google.cloud.biglake.hive.v1beta.HiveMetastoreService.UpdateHiveDatabase</code><br />
<code dir="ltr" translate="no">google.cloud.biglake.hive.v1beta.HiveMetastoreService.UpdateHiveTable</code><br />
<code dir="ltr" translate="no">google.cloud.biglake.v1.DeltaSharingService.CreateDeltaSharingCatalog</code><br />
<code dir="ltr" translate="no">google.cloud.biglake.v1.DeltaSharingService.DeleteDeltaSharingCatalog</code><br />
<code dir="ltr" translate="no">google.cloud.biglake.v1.DeltaSharingService.UpdateDeltaSharingCatalog</code><br />
<code dir="ltr" translate="no">google.cloud.biglake.v1.IcebergCatalogIamService.SetIcebergCatalogIamPolicy</code><br />
<code dir="ltr" translate="no">google.cloud.biglake.v1.IcebergCatalogIamService.SetIcebergNamespaceIamPolicy</code><br />
<code dir="ltr" translate="no">google.cloud.biglake.v1.IcebergCatalogIamService.SetIcebergTableIamPolicy</code><br />
<code dir="ltr" translate="no">google.cloud.biglake.v1.IcebergCatalogService.CreateIcebergCatalog</code><br />
<code dir="ltr" translate="no">google.cloud.biglake.v1.IcebergCatalogService.CreateIcebergNamespace</code><br />
<code dir="ltr" translate="no">google.cloud.biglake.v1.IcebergCatalogService.CreateIcebergTable</code><br />
<code dir="ltr" translate="no">google.cloud.biglake.v1.IcebergCatalogService.DeleteIcebergCatalog</code><br />
<code dir="ltr" translate="no">google.cloud.biglake.v1.IcebergCatalogService.DeleteIcebergNamespace</code><br />
<code dir="ltr" translate="no">google.cloud.biglake.v1.IcebergCatalogService.DeleteIcebergTable</code><br />
<code dir="ltr" translate="no">google.cloud.biglake.v1.IcebergCatalogService.GetIcebergCatalogConfig</code><br />
<code dir="ltr" translate="no">google.cloud.biglake.v1.IcebergCatalogService.UpdateIcebergCatalog</code><br />
<code dir="ltr" translate="no">google.cloud.biglake.v1.IcebergCatalogService.UpdateIcebergNamespace</code><br />
<code dir="ltr" translate="no">google.cloud.biglake.v1.IcebergCatalogService.UpdateIcebergTable</code><br />
<code dir="ltr" translate="no">google.cloud.biglake.v1alpha.DeltaSharingService.CreateDeltaSharingCatalog</code><br />
<code dir="ltr" translate="no">google.cloud.biglake.v1alpha.DeltaSharingService.UpdateDeltaSharingCatalog</code><br />
<code dir="ltr" translate="no">google.cloud.biglake.v1alpha.IcebergCatalogService.CreateIcebergCatalog</code><br />
<code dir="ltr" translate="no">google.cloud.biglake.v1beta.IcebergCatalogService.CreateIcebergCatalog</code><br />
<code dir="ltr" translate="no">google.cloud.biglake.v1beta.IcebergCatalogService.CreateIcebergNamespace</code><br />
<code dir="ltr" translate="no">google.cloud.biglake.v1beta.IcebergCatalogService.CreateIcebergTable</code><br />
<code dir="ltr" translate="no">google.cloud.biglake.v1beta.IcebergCatalogService.DeleteIcebergCatalog</code><br />
<code dir="ltr" translate="no">google.cloud.biglake.v1beta.IcebergCatalogService.DeleteIcebergNamespace</code><br />
<code dir="ltr" translate="no">google.cloud.biglake.v1beta.IcebergCatalogService.DeleteIcebergTable</code><br />
<code dir="ltr" translate="no">google.cloud.biglake.v1beta.IcebergCatalogService.UpdateIcebergCatalog</code><br />
<code dir="ltr" translate="no">google.cloud.biglake.v1beta.IcebergCatalogService.UpdateIcebergNamespace</code><br />
<code dir="ltr" translate="no">google.cloud.biglake.v1beta.IcebergCatalogService.UpdateIcebergTable</code><br />
<code dir="ltr" translate="no">google.cloud.bigquery.biglake.v1.MetastoreService.CreateCatalog</code><br />
<code dir="ltr" translate="no">google.cloud.bigquery.biglake.v1.MetastoreService.CreateDatabase</code><br />
<code dir="ltr" translate="no">google.cloud.bigquery.biglake.v1.MetastoreService.CreateTable</code><br />
<code dir="ltr" translate="no">google.cloud.bigquery.biglake.v1.MetastoreService.DeleteCatalog</code><br />
<code dir="ltr" translate="no">google.cloud.bigquery.biglake.v1.MetastoreService.DeleteDatabase</code><br />
<code dir="ltr" translate="no">google.cloud.bigquery.biglake.v1.MetastoreService.DeleteTable</code><br />
<code dir="ltr" translate="no">google.cloud.bigquery.biglake.v1.MetastoreService.RenameTable</code><br />
<code dir="ltr" translate="no">google.cloud.bigquery.biglake.v1.MetastoreService.UpdateDatabase</code><br />
<code dir="ltr" translate="no">google.cloud.bigquery.biglake.v1.MetastoreService.UpdateTable</code><br />
<code dir="ltr" translate="no">google.cloud.bigquery.biglake.v1alpha1.MetastoreService.CheckLock</code><br />
<code dir="ltr" translate="no">google.cloud.bigquery.biglake.v1alpha1.MetastoreService.CreateCatalog</code><br />
<code dir="ltr" translate="no">google.cloud.bigquery.biglake.v1alpha1.MetastoreService.CreateDatabase</code><br />
<code dir="ltr" translate="no">google.cloud.bigquery.biglake.v1alpha1.MetastoreService.CreateLock</code><br />
<code dir="ltr" translate="no">google.cloud.bigquery.biglake.v1alpha1.MetastoreService.CreateTable</code><br />
<code dir="ltr" translate="no">google.cloud.bigquery.biglake.v1alpha1.MetastoreService.DeleteCatalog</code><br />
<code dir="ltr" translate="no">google.cloud.bigquery.biglake.v1alpha1.MetastoreService.DeleteDatabase</code><br />
<code dir="ltr" translate="no">google.cloud.bigquery.biglake.v1alpha1.MetastoreService.DeleteLock</code><br />
<code dir="ltr" translate="no">google.cloud.bigquery.biglake.v1alpha1.MetastoreService.DeleteTable</code><br />
<code dir="ltr" translate="no">google.cloud.bigquery.biglake.v1alpha1.MetastoreService.RenameTable</code><br />
<code dir="ltr" translate="no">google.cloud.bigquery.biglake.v1alpha1.MetastoreService.UpdateDatabase</code><br />
<code dir="ltr" translate="no">google.cloud.bigquery.biglake.v1alpha1.MetastoreService.UpdateTable</code></td>
</tr>
</tbody>
</table>

## API interface audit logs

For information about how and which permissions are evaluated for each method, see the Identity and Access Management documentation for Lakehouse.

### `google.cloud.biglake.hive.v1alpha.HiveMetastoreService`

The following audit logs are associated with methods belonging to `google.cloud.biglake.hive.v1alpha.HiveMetastoreService` .

#### `BatchCreatePartitions`

  - **Method** : `google.cloud.biglake.hive.v1alpha.HiveMetastoreService.BatchCreatePartitions`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.tables.createPartitions - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.biglake.hive.v1alpha.HiveMetastoreService.BatchCreatePartitions"`  

#### `BatchDeletePartitions`

  - **Method** : `google.cloud.biglake.hive.v1alpha.HiveMetastoreService.BatchDeletePartitions`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.tables.deletePartitions - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.biglake.hive.v1alpha.HiveMetastoreService.BatchDeletePartitions"`  

#### `BatchUpdatePartitions`

  - **Method** : `google.cloud.biglake.hive.v1alpha.HiveMetastoreService.BatchUpdatePartitions`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.tables.updatePartitions - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.biglake.hive.v1alpha.HiveMetastoreService.BatchUpdatePartitions"`  

#### `CreateHiveCatalog`

  - **Method** : `google.cloud.biglake.hive.v1alpha.HiveMetastoreService.CreateHiveCatalog`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.catalogs.create - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.biglake.hive.v1alpha.HiveMetastoreService.CreateHiveCatalog"`  

#### `CreateHiveDatabase`

  - **Method** : `google.cloud.biglake.hive.v1alpha.HiveMetastoreService.CreateHiveDatabase`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.namespaces.create - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.biglake.hive.v1alpha.HiveMetastoreService.CreateHiveDatabase"`  

#### `CreateHiveTable`

  - **Method** : `google.cloud.biglake.hive.v1alpha.HiveMetastoreService.CreateHiveTable`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.tables.create - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.biglake.hive.v1alpha.HiveMetastoreService.CreateHiveTable"`  

#### `DeleteHiveCatalog`

  - **Method** : `google.cloud.biglake.hive.v1alpha.HiveMetastoreService.DeleteHiveCatalog`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.catalogs.delete - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.biglake.hive.v1alpha.HiveMetastoreService.DeleteHiveCatalog"`  

#### `DeleteHiveDatabase`

  - **Method** : `google.cloud.biglake.hive.v1alpha.HiveMetastoreService.DeleteHiveDatabase`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.namespaces.delete - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.biglake.hive.v1alpha.HiveMetastoreService.DeleteHiveDatabase"`  

#### `DeleteHiveTable`

  - **Method** : `google.cloud.biglake.hive.v1alpha.HiveMetastoreService.DeleteHiveTable`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.tables.delete - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.biglake.hive.v1alpha.HiveMetastoreService.DeleteHiveTable"`  

#### `GetHiveCatalog`

  - **Method** : `google.cloud.biglake.hive.v1alpha.HiveMetastoreService.GetHiveCatalog`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.catalogs.get - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.biglake.hive.v1alpha.HiveMetastoreService.GetHiveCatalog"`  

#### `GetHiveDatabase`

  - **Method** : `google.cloud.biglake.hive.v1alpha.HiveMetastoreService.GetHiveDatabase`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.namespaces.get - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.biglake.hive.v1alpha.HiveMetastoreService.GetHiveDatabase"`  

#### `GetHiveTable`

  - **Method** : `google.cloud.biglake.hive.v1alpha.HiveMetastoreService.GetHiveTable`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.tables.get - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.biglake.hive.v1alpha.HiveMetastoreService.GetHiveTable"`  

#### `ListHiveDatabases`

  - **Method** : `google.cloud.biglake.hive.v1alpha.HiveMetastoreService.ListHiveDatabases`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.namespaces.list - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.biglake.hive.v1alpha.HiveMetastoreService.ListHiveDatabases"`  

#### `ListHiveTables`

  - **Method** : `google.cloud.biglake.hive.v1alpha.HiveMetastoreService.ListHiveTables`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.tables.list - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.biglake.hive.v1alpha.HiveMetastoreService.ListHiveTables"`  

#### `ListPartitions`

  - **Method** : `google.cloud.biglake.hive.v1alpha.HiveMetastoreService.ListPartitions`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.tables.listPartitions - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : [**Streaming RPC**](https://docs.cloud.google.com/logging/docs/audit/understanding-audit-logs#streaming)  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.biglake.hive.v1alpha.HiveMetastoreService.ListPartitions"`  

#### `UpdateHiveCatalog`

  - **Method** : `google.cloud.biglake.hive.v1alpha.HiveMetastoreService.UpdateHiveCatalog`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.catalogs.update - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.biglake.hive.v1alpha.HiveMetastoreService.UpdateHiveCatalog"`  

#### `UpdateHiveDatabase`

  - **Method** : `google.cloud.biglake.hive.v1alpha.HiveMetastoreService.UpdateHiveDatabase`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.namespaces.update - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.biglake.hive.v1alpha.HiveMetastoreService.UpdateHiveDatabase"`  

#### `UpdateHiveTable`

  - **Method** : `google.cloud.biglake.hive.v1alpha.HiveMetastoreService.UpdateHiveTable`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.tables.update - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.biglake.hive.v1alpha.HiveMetastoreService.UpdateHiveTable"`  

### `google.cloud.biglake.hive.v1beta.HiveMetastoreService`

The following audit logs are associated with methods belonging to `google.cloud.biglake.hive.v1beta.HiveMetastoreService` .

#### `BatchCreatePartitions`

  - **Method** : `google.cloud.biglake.hive.v1beta.HiveMetastoreService.BatchCreatePartitions`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.tables.createPartitions - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.biglake.hive.v1beta.HiveMetastoreService.BatchCreatePartitions"`  

#### `BatchDeletePartitions`

  - **Method** : `google.cloud.biglake.hive.v1beta.HiveMetastoreService.BatchDeletePartitions`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.tables.deletePartitions - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.biglake.hive.v1beta.HiveMetastoreService.BatchDeletePartitions"`  

#### `BatchUpdatePartitions`

  - **Method** : `google.cloud.biglake.hive.v1beta.HiveMetastoreService.BatchUpdatePartitions`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.tables.updatePartitions - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.biglake.hive.v1beta.HiveMetastoreService.BatchUpdatePartitions"`  

#### `CreateHiveCatalog`

  - **Method** : `google.cloud.biglake.hive.v1beta.HiveMetastoreService.CreateHiveCatalog`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.catalogs.create - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.biglake.hive.v1beta.HiveMetastoreService.CreateHiveCatalog"`  

#### `CreateHiveDatabase`

  - **Method** : `google.cloud.biglake.hive.v1beta.HiveMetastoreService.CreateHiveDatabase`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.namespaces.create - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.biglake.hive.v1beta.HiveMetastoreService.CreateHiveDatabase"`  

#### `CreateHiveTable`

  - **Method** : `google.cloud.biglake.hive.v1beta.HiveMetastoreService.CreateHiveTable`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.tables.create - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.biglake.hive.v1beta.HiveMetastoreService.CreateHiveTable"`  

#### `DeleteHiveCatalog`

  - **Method** : `google.cloud.biglake.hive.v1beta.HiveMetastoreService.DeleteHiveCatalog`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.catalogs.delete - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.biglake.hive.v1beta.HiveMetastoreService.DeleteHiveCatalog"`  

#### `DeleteHiveDatabase`

  - **Method** : `google.cloud.biglake.hive.v1beta.HiveMetastoreService.DeleteHiveDatabase`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.namespaces.delete - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.biglake.hive.v1beta.HiveMetastoreService.DeleteHiveDatabase"`  

#### `DeleteHiveTable`

  - **Method** : `google.cloud.biglake.hive.v1beta.HiveMetastoreService.DeleteHiveTable`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.tables.delete - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.biglake.hive.v1beta.HiveMetastoreService.DeleteHiveTable"`  

#### `GetHiveCatalog`

  - **Method** : `google.cloud.biglake.hive.v1beta.HiveMetastoreService.GetHiveCatalog`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.catalogs.get - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.biglake.hive.v1beta.HiveMetastoreService.GetHiveCatalog"`  

#### `GetHiveDatabase`

  - **Method** : `google.cloud.biglake.hive.v1beta.HiveMetastoreService.GetHiveDatabase`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.namespaces.get - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.biglake.hive.v1beta.HiveMetastoreService.GetHiveDatabase"`  

#### `GetHiveTable`

  - **Method** : `google.cloud.biglake.hive.v1beta.HiveMetastoreService.GetHiveTable`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.tables.get - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.biglake.hive.v1beta.HiveMetastoreService.GetHiveTable"`  

#### `ListHiveDatabases`

  - **Method** : `google.cloud.biglake.hive.v1beta.HiveMetastoreService.ListHiveDatabases`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.namespaces.list - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.biglake.hive.v1beta.HiveMetastoreService.ListHiveDatabases"`  

#### `ListHiveTables`

  - **Method** : `google.cloud.biglake.hive.v1beta.HiveMetastoreService.ListHiveTables`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.tables.list - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.biglake.hive.v1beta.HiveMetastoreService.ListHiveTables"`  

#### `ListPartitions`

  - **Method** : `google.cloud.biglake.hive.v1beta.HiveMetastoreService.ListPartitions`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.tables.listPartitions - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : [**Streaming RPC**](https://docs.cloud.google.com/logging/docs/audit/understanding-audit-logs#streaming)  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.biglake.hive.v1beta.HiveMetastoreService.ListPartitions"`  

#### `UpdateHiveCatalog`

  - **Method** : `google.cloud.biglake.hive.v1beta.HiveMetastoreService.UpdateHiveCatalog`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.catalogs.update - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.biglake.hive.v1beta.HiveMetastoreService.UpdateHiveCatalog"`  

#### `UpdateHiveDatabase`

  - **Method** : `google.cloud.biglake.hive.v1beta.HiveMetastoreService.UpdateHiveDatabase`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.namespaces.update - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.biglake.hive.v1beta.HiveMetastoreService.UpdateHiveDatabase"`  

#### `UpdateHiveTable`

  - **Method** : `google.cloud.biglake.hive.v1beta.HiveMetastoreService.UpdateHiveTable`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.tables.update - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.biglake.hive.v1beta.HiveMetastoreService.UpdateHiveTable"`  

### `google.cloud.biglake.v1.DeltaSharingService`

The following audit logs are associated with methods belonging to `google.cloud.biglake.v1.DeltaSharingService` .

#### `CreateDeltaSharingCatalog`

  - **Method** : `google.cloud.biglake.v1.DeltaSharingService.CreateDeltaSharingCatalog`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.catalogs.create - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.biglake.v1.DeltaSharingService.CreateDeltaSharingCatalog"`  

#### `DeleteDeltaSharingCatalog`

  - **Method** : `google.cloud.biglake.v1.DeltaSharingService.DeleteDeltaSharingCatalog`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.catalogs.delete - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.biglake.v1.DeltaSharingService.DeleteDeltaSharingCatalog"`  

#### `GetDeltaSharingCatalog`

  - **Method** : `google.cloud.biglake.v1.DeltaSharingService.GetDeltaSharingCatalog`  
  - **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
  - **Permissions** :
      - `biglake.catalogs.get - ADMIN_READ`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.biglake.v1.DeltaSharingService.GetDeltaSharingCatalog"`  

#### `ListDeltaSharingShares`

  - **Method** : `google.cloud.biglake.v1.DeltaSharingService.ListDeltaSharingShares`  
  - **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
  - **Permissions** :
      - `biglake.catalogs.get - ADMIN_READ`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.biglake.v1.DeltaSharingService.ListDeltaSharingShares"`  

#### `ListDeltaSharingTables`

  - **Method** : `google.cloud.biglake.v1.DeltaSharingService.ListDeltaSharingTables`  
  - **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
  - **Permissions** :
      - `biglake.namespaces.get - ADMIN_READ`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.biglake.v1.DeltaSharingService.ListDeltaSharingTables"`  

#### `UpdateDeltaSharingCatalog`

  - **Method** : `google.cloud.biglake.v1.DeltaSharingService.UpdateDeltaSharingCatalog`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.catalogs.update - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.biglake.v1.DeltaSharingService.UpdateDeltaSharingCatalog"`  

### `google.cloud.biglake.v1.IcebergCatalogIamService`

The following audit logs are associated with methods belonging to `google.cloud.biglake.v1.IcebergCatalogIamService` .

#### `SetIcebergCatalogIamPolicy`

  - **Method** : `google.cloud.biglake.v1.IcebergCatalogIamService.SetIcebergCatalogIamPolicy`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.catalogs.setIamPolicy - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.biglake.v1.IcebergCatalogIamService.SetIcebergCatalogIamPolicy"`  

#### `SetIcebergNamespaceIamPolicy`

  - **Method** : `google.cloud.biglake.v1.IcebergCatalogIamService.SetIcebergNamespaceIamPolicy`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.namespaces.setIamPolicy - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.biglake.v1.IcebergCatalogIamService.SetIcebergNamespaceIamPolicy"`  

#### `SetIcebergTableIamPolicy`

  - **Method** : `google.cloud.biglake.v1.IcebergCatalogIamService.SetIcebergTableIamPolicy`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.tables.setIamPolicy - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.biglake.v1.IcebergCatalogIamService.SetIcebergTableIamPolicy"`  

### `google.cloud.biglake.v1.IcebergCatalogService`

The following audit logs are associated with methods belonging to `google.cloud.biglake.v1.IcebergCatalogService` .

#### `CreateIcebergCatalog`

  - **Method** : `google.cloud.biglake.v1.IcebergCatalogService.CreateIcebergCatalog`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.catalogs.create - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.biglake.v1.IcebergCatalogService.CreateIcebergCatalog"`  

#### `CreateIcebergNamespace`

  - **Method** : `google.cloud.biglake.v1.IcebergCatalogService.CreateIcebergNamespace`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.namespaces.create - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.biglake.v1.IcebergCatalogService.CreateIcebergNamespace"`  

#### `CreateIcebergTable`

  - **Method** : `google.cloud.biglake.v1.IcebergCatalogService.CreateIcebergTable`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.tables.create - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.biglake.v1.IcebergCatalogService.CreateIcebergTable"`  

#### `DeleteIcebergCatalog`

  - **Method** : `google.cloud.biglake.v1.IcebergCatalogService.DeleteIcebergCatalog`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.catalogs.delete - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.biglake.v1.IcebergCatalogService.DeleteIcebergCatalog"`  

#### `DeleteIcebergNamespace`

  - **Method** : `google.cloud.biglake.v1.IcebergCatalogService.DeleteIcebergNamespace`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.namespaces.delete - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.biglake.v1.IcebergCatalogService.DeleteIcebergNamespace"`  

#### `DeleteIcebergTable`

  - **Method** : `google.cloud.biglake.v1.IcebergCatalogService.DeleteIcebergTable`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.tables.delete - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.biglake.v1.IcebergCatalogService.DeleteIcebergTable"`  

#### `GetIcebergCatalogConfig`

  - **Method** : `google.cloud.biglake.v1.IcebergCatalogService.GetIcebergCatalogConfig`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.catalogs.get - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.biglake.v1.IcebergCatalogService.GetIcebergCatalogConfig"`  

#### `UpdateIcebergCatalog`

  - **Method** : `google.cloud.biglake.v1.IcebergCatalogService.UpdateIcebergCatalog`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.catalogs.update - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.biglake.v1.IcebergCatalogService.UpdateIcebergCatalog"`  

#### `UpdateIcebergNamespace`

  - **Method** : `google.cloud.biglake.v1.IcebergCatalogService.UpdateIcebergNamespace`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.namespaces.update - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.biglake.v1.IcebergCatalogService.UpdateIcebergNamespace"`  

#### `UpdateIcebergTable`

  - **Method** : `google.cloud.biglake.v1.IcebergCatalogService.UpdateIcebergTable`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.tables.update - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.biglake.v1.IcebergCatalogService.UpdateIcebergTable"`  

### `google.cloud.biglake.v1alpha.DeltaSharingService`

The following audit logs are associated with methods belonging to `google.cloud.biglake.v1alpha.DeltaSharingService` .

#### `CreateDeltaSharingCatalog`

  - **Method** : `google.cloud.biglake.v1alpha.DeltaSharingService.CreateDeltaSharingCatalog`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.catalogs.create - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.biglake.v1alpha.DeltaSharingService.CreateDeltaSharingCatalog"`  

#### `GetDeltaSharingCatalog`

  - **Method** : `google.cloud.biglake.v1alpha.DeltaSharingService.GetDeltaSharingCatalog`  
  - **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
  - **Permissions** :
      - `biglake.catalogs.get - ADMIN_READ`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.biglake.v1alpha.DeltaSharingService.GetDeltaSharingCatalog"`  

#### `UpdateDeltaSharingCatalog`

  - **Method** : `google.cloud.biglake.v1alpha.DeltaSharingService.UpdateDeltaSharingCatalog`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.catalogs.update - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.biglake.v1alpha.DeltaSharingService.UpdateDeltaSharingCatalog"`  

### `google.cloud.biglake.v1alpha.IcebergCatalogService`

The following audit logs are associated with methods belonging to `google.cloud.biglake.v1alpha.IcebergCatalogService` .

#### `CreateIcebergCatalog`

  - **Method** : `google.cloud.biglake.v1alpha.IcebergCatalogService.CreateIcebergCatalog`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.catalogs.create - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.biglake.v1alpha.IcebergCatalogService.CreateIcebergCatalog"`  

### `google.cloud.biglake.v1beta.IcebergCatalogService`

The following audit logs are associated with methods belonging to `google.cloud.biglake.v1beta.IcebergCatalogService` .

#### `CreateIcebergCatalog`

  - **Method** : `google.cloud.biglake.v1beta.IcebergCatalogService.CreateIcebergCatalog`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.catalogs.create - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.biglake.v1beta.IcebergCatalogService.CreateIcebergCatalog"`  

#### `CreateIcebergNamespace`

  - **Method** : `google.cloud.biglake.v1beta.IcebergCatalogService.CreateIcebergNamespace`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.namespaces.create - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.biglake.v1beta.IcebergCatalogService.CreateIcebergNamespace"`  

#### `CreateIcebergTable`

  - **Method** : `google.cloud.biglake.v1beta.IcebergCatalogService.CreateIcebergTable`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.tables.create - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.biglake.v1beta.IcebergCatalogService.CreateIcebergTable"`  

#### `DeleteIcebergCatalog`

  - **Method** : `google.cloud.biglake.v1beta.IcebergCatalogService.DeleteIcebergCatalog`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.catalogs.delete - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.biglake.v1beta.IcebergCatalogService.DeleteIcebergCatalog"`  

#### `DeleteIcebergNamespace`

  - **Method** : `google.cloud.biglake.v1beta.IcebergCatalogService.DeleteIcebergNamespace`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.namespaces.delete - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.biglake.v1beta.IcebergCatalogService.DeleteIcebergNamespace"`  

#### `DeleteIcebergTable`

  - **Method** : `google.cloud.biglake.v1beta.IcebergCatalogService.DeleteIcebergTable`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.tables.delete - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.biglake.v1beta.IcebergCatalogService.DeleteIcebergTable"`  

#### `UpdateIcebergCatalog`

  - **Method** : `google.cloud.biglake.v1beta.IcebergCatalogService.UpdateIcebergCatalog`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.catalogs.update - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.biglake.v1beta.IcebergCatalogService.UpdateIcebergCatalog"`  

#### `UpdateIcebergNamespace`

  - **Method** : `google.cloud.biglake.v1beta.IcebergCatalogService.UpdateIcebergNamespace`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.namespaces.update - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.biglake.v1beta.IcebergCatalogService.UpdateIcebergNamespace"`  

#### `UpdateIcebergTable`

  - **Method** : `google.cloud.biglake.v1beta.IcebergCatalogService.UpdateIcebergTable`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.tables.update - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.biglake.v1beta.IcebergCatalogService.UpdateIcebergTable"`  

### `google.cloud.bigquery.biglake.v1.MetastoreService`

The following audit logs are associated with methods belonging to `google.cloud.bigquery.biglake.v1.MetastoreService` .

#### `CreateCatalog`

  - **Method** : `google.cloud.bigquery.biglake.v1.MetastoreService.CreateCatalog`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.catalogs.create - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.bigquery.biglake.v1.MetastoreService.CreateCatalog"`  

#### `CreateDatabase`

  - **Method** : `google.cloud.bigquery.biglake.v1.MetastoreService.CreateDatabase`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.databases.create - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.bigquery.biglake.v1.MetastoreService.CreateDatabase"`  

#### `CreateTable`

  - **Method** : `google.cloud.bigquery.biglake.v1.MetastoreService.CreateTable`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.tables.create - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.bigquery.biglake.v1.MetastoreService.CreateTable"`  

#### `DeleteCatalog`

  - **Method** : `google.cloud.bigquery.biglake.v1.MetastoreService.DeleteCatalog`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.catalogs.delete - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.bigquery.biglake.v1.MetastoreService.DeleteCatalog"`  

#### `DeleteDatabase`

  - **Method** : `google.cloud.bigquery.biglake.v1.MetastoreService.DeleteDatabase`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.databases.delete - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.bigquery.biglake.v1.MetastoreService.DeleteDatabase"`  

#### `DeleteTable`

  - **Method** : `google.cloud.bigquery.biglake.v1.MetastoreService.DeleteTable`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.tables.delete - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.bigquery.biglake.v1.MetastoreService.DeleteTable"`  

#### `GetCatalog`

  - **Method** : `google.cloud.bigquery.biglake.v1.MetastoreService.GetCatalog`  
  - **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
  - **Permissions** :
      - `biglake.catalogs.get - ADMIN_READ`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.bigquery.biglake.v1.MetastoreService.GetCatalog"`  

#### `GetDatabase`

  - **Method** : `google.cloud.bigquery.biglake.v1.MetastoreService.GetDatabase`  
  - **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
  - **Permissions** :
      - `biglake.databases.get - ADMIN_READ`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.bigquery.biglake.v1.MetastoreService.GetDatabase"`  

#### `GetTable`

  - **Method** : `google.cloud.bigquery.biglake.v1.MetastoreService.GetTable`  
  - **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
  - **Permissions** :
      - `biglake.tables.get - ADMIN_READ`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.bigquery.biglake.v1.MetastoreService.GetTable"`  

#### `ListCatalogs`

  - **Method** : `google.cloud.bigquery.biglake.v1.MetastoreService.ListCatalogs`  
  - **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
  - **Permissions** :
      - `biglake.catalogs.list - ADMIN_READ`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.bigquery.biglake.v1.MetastoreService.ListCatalogs"`  

#### `ListDatabases`

  - **Method** : `google.cloud.bigquery.biglake.v1.MetastoreService.ListDatabases`  
  - **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
  - **Permissions** :
      - `biglake.databases.list - ADMIN_READ`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.bigquery.biglake.v1.MetastoreService.ListDatabases"`  

#### `ListTables`

  - **Method** : `google.cloud.bigquery.biglake.v1.MetastoreService.ListTables`  
  - **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
  - **Permissions** :
      - `biglake.tables.list - ADMIN_READ`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.bigquery.biglake.v1.MetastoreService.ListTables"`  

#### `RenameTable`

  - **Method** : `google.cloud.bigquery.biglake.v1.MetastoreService.RenameTable`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.tables.update - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.bigquery.biglake.v1.MetastoreService.RenameTable"`  

#### `UpdateDatabase`

  - **Method** : `google.cloud.bigquery.biglake.v1.MetastoreService.UpdateDatabase`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.databases.update - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.bigquery.biglake.v1.MetastoreService.UpdateDatabase"`  

#### `UpdateTable`

  - **Method** : `google.cloud.bigquery.biglake.v1.MetastoreService.UpdateTable`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.tables.update - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.bigquery.biglake.v1.MetastoreService.UpdateTable"`  

### `google.cloud.bigquery.biglake.v1alpha1.MetastoreService`

The following audit logs are associated with methods belonging to `google.cloud.bigquery.biglake.v1alpha1.MetastoreService` .

#### `CheckLock`

  - **Method** : `google.cloud.bigquery.biglake.v1alpha1.MetastoreService.CheckLock`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.locks.check - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.bigquery.biglake.v1alpha1.MetastoreService.CheckLock"`  

#### `CreateCatalog`

  - **Method** : `google.cloud.bigquery.biglake.v1alpha1.MetastoreService.CreateCatalog`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.catalogs.create - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.bigquery.biglake.v1alpha1.MetastoreService.CreateCatalog"`  

#### `CreateDatabase`

  - **Method** : `google.cloud.bigquery.biglake.v1alpha1.MetastoreService.CreateDatabase`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.databases.create - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.bigquery.biglake.v1alpha1.MetastoreService.CreateDatabase"`  

#### `CreateLock`

  - **Method** : `google.cloud.bigquery.biglake.v1alpha1.MetastoreService.CreateLock`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.locks.create - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.bigquery.biglake.v1alpha1.MetastoreService.CreateLock"`  

#### `CreateTable`

  - **Method** : `google.cloud.bigquery.biglake.v1alpha1.MetastoreService.CreateTable`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.tables.create - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.bigquery.biglake.v1alpha1.MetastoreService.CreateTable"`  

#### `DeleteCatalog`

  - **Method** : `google.cloud.bigquery.biglake.v1alpha1.MetastoreService.DeleteCatalog`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.catalogs.delete - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.bigquery.biglake.v1alpha1.MetastoreService.DeleteCatalog"`  

#### `DeleteDatabase`

  - **Method** : `google.cloud.bigquery.biglake.v1alpha1.MetastoreService.DeleteDatabase`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.databases.delete - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.bigquery.biglake.v1alpha1.MetastoreService.DeleteDatabase"`  

#### `DeleteLock`

  - **Method** : `google.cloud.bigquery.biglake.v1alpha1.MetastoreService.DeleteLock`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.locks.delete - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.bigquery.biglake.v1alpha1.MetastoreService.DeleteLock"`  

#### `DeleteTable`

  - **Method** : `google.cloud.bigquery.biglake.v1alpha1.MetastoreService.DeleteTable`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.tables.delete - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.bigquery.biglake.v1alpha1.MetastoreService.DeleteTable"`  

#### `GetCatalog`

  - **Method** : `google.cloud.bigquery.biglake.v1alpha1.MetastoreService.GetCatalog`  
  - **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
  - **Permissions** :
      - `biglake.catalogs.get - ADMIN_READ`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.bigquery.biglake.v1alpha1.MetastoreService.GetCatalog"`  

#### `GetDatabase`

  - **Method** : `google.cloud.bigquery.biglake.v1alpha1.MetastoreService.GetDatabase`  
  - **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
  - **Permissions** :
      - `biglake.databases.get - ADMIN_READ`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.bigquery.biglake.v1alpha1.MetastoreService.GetDatabase"`  

#### `GetTable`

  - **Method** : `google.cloud.bigquery.biglake.v1alpha1.MetastoreService.GetTable`  
  - **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
  - **Permissions** :
      - `biglake.tables.get - ADMIN_READ`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.bigquery.biglake.v1alpha1.MetastoreService.GetTable"`  

#### `ListCatalogs`

  - **Method** : `google.cloud.bigquery.biglake.v1alpha1.MetastoreService.ListCatalogs`  
  - **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
  - **Permissions** :
      - `biglake.catalogs.list - ADMIN_READ`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.bigquery.biglake.v1alpha1.MetastoreService.ListCatalogs"`  

#### `ListDatabases`

  - **Method** : `google.cloud.bigquery.biglake.v1alpha1.MetastoreService.ListDatabases`  
  - **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
  - **Permissions** :
      - `biglake.databases.list - ADMIN_READ`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.bigquery.biglake.v1alpha1.MetastoreService.ListDatabases"`  

#### `ListLocks`

  - **Method** : `google.cloud.bigquery.biglake.v1alpha1.MetastoreService.ListLocks`  
  - **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
  - **Permissions** :
      - `biglake.locks.list - ADMIN_READ`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.bigquery.biglake.v1alpha1.MetastoreService.ListLocks"`  

#### `ListTables`

  - **Method** : `google.cloud.bigquery.biglake.v1alpha1.MetastoreService.ListTables`  
  - **Audit log type** : [Data access](https://docs.cloud.google.com/logging/docs/audit#data-access)  
  - **Permissions** :
      - `biglake.tables.list - ADMIN_READ`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.bigquery.biglake.v1alpha1.MetastoreService.ListTables"`  

#### `RenameTable`

  - **Method** : `google.cloud.bigquery.biglake.v1alpha1.MetastoreService.RenameTable`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.tables.update - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.bigquery.biglake.v1alpha1.MetastoreService.RenameTable"`  

#### `UpdateDatabase`

  - **Method** : `google.cloud.bigquery.biglake.v1alpha1.MetastoreService.UpdateDatabase`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.databases.update - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.bigquery.biglake.v1alpha1.MetastoreService.UpdateDatabase"`  

#### `UpdateTable`

  - **Method** : `google.cloud.bigquery.biglake.v1alpha1.MetastoreService.UpdateTable`  
  - **Audit log type** : [Admin activity](https://docs.cloud.google.com/logging/docs/audit#admin-activity)  
  - **Permissions** :
      - `biglake.tables.update - ADMIN_WRITE`
  - **Method is a long-running or streaming operation** : No.  
  - **Filter for this method** : `protoPayload.methodName="google.cloud.bigquery.biglake.v1alpha1.MetastoreService.UpdateTable"`  

## Methods that don't produce audit logs

A method might not produce audit logs for one or more of the following reasons:

  - It is a high volume method involving significant log generation and storage costs.
  - It has low auditing value.
  - Another audit or platform log already provides method coverage.

The following methods don't produce audit logs:

  - `google.cloud.biglake.hive.v1alpha.HiveMetastoreService.ListHiveCatalogs`
  - `google.cloud.biglake.hive.v1beta.HiveMetastoreService.ListHiveCatalogs`
  - `google.cloud.biglake.v1.DeltaSharingService.ListDeltaSharingCatalogs`
  - `google.cloud.biglake.v1.DeltaSharingService.ListDeltaSharingSchemas`
  - `google.cloud.biglake.v1alpha.DeltaSharingService.DeleteDeltaSharingCatalog`
  - `google.cloud.biglake.v1alpha.DeltaSharingService.ListDeltaSharingCatalogs`
  - `google.cloud.biglake.v1alpha.DeltaSharingService.ListDeltaSharingSchemas`
  - `google.cloud.biglake.v1alpha.DeltaSharingService.ListDeltaSharingShares`
  - `google.cloud.biglake.v1alpha.DeltaSharingService.ListDeltaSharingTables`
  - `google.cloud.biglake.v1alpha.IcebergCatalogService.CheckIcebergNamespaceExists`
  - `google.cloud.biglake.v1alpha.IcebergCatalogService.CheckIcebergTableExists`
  - `google.cloud.biglake.v1alpha.IcebergCatalogService.CreateIcebergNamespace`
  - `google.cloud.biglake.v1alpha.IcebergCatalogService.CreateIcebergTable`
  - `google.cloud.biglake.v1alpha.IcebergCatalogService.DeleteIcebergCatalog`
  - `google.cloud.biglake.v1alpha.IcebergCatalogService.DeleteIcebergNamespace`
  - `google.cloud.biglake.v1alpha.IcebergCatalogService.DeleteIcebergTable`
  - `google.cloud.biglake.v1alpha.IcebergCatalogService.FailoverIcebergCatalog`
  - `google.cloud.biglake.v1alpha.IcebergCatalogService.GetIcebergCatalog`
  - `google.cloud.biglake.v1alpha.IcebergCatalogService.GetIcebergCatalogConfig`
  - `google.cloud.biglake.v1alpha.IcebergCatalogService.GetIcebergNamespace`
  - `google.cloud.biglake.v1alpha.IcebergCatalogService.GetIcebergTable`
  - `google.cloud.biglake.v1alpha.IcebergCatalogService.ListIcebergCatalogs`
  - `google.cloud.biglake.v1alpha.IcebergCatalogService.ListIcebergNamespaces`
  - `google.cloud.biglake.v1alpha.IcebergCatalogService.ListIcebergTableIdentifiers`
  - `google.cloud.biglake.v1alpha.IcebergCatalogService.LoadIcebergTableCredentials`
  - `google.cloud.biglake.v1alpha.IcebergCatalogService.RegisterIcebergTable`
  - `google.cloud.biglake.v1alpha.IcebergCatalogService.ReportIcebergTableMetrics`
  - `google.cloud.biglake.v1alpha.IcebergCatalogService.UpdateIcebergCatalog`
  - `google.cloud.biglake.v1alpha.IcebergCatalogService.UpdateIcebergNamespace`
  - `google.cloud.biglake.v1alpha.IcebergCatalogService.UpdateIcebergTable`
  - `google.cloud.biglake.v1beta.IcebergCatalogService.CheckIcebergNamespaceExists`
  - `google.cloud.biglake.v1beta.IcebergCatalogService.CheckIcebergTableExists`
  - `google.cloud.biglake.v1beta.IcebergCatalogService.FailoverIcebergCatalog`
  - `google.cloud.biglake.v1beta.IcebergCatalogService.GetIcebergCatalog`
  - `google.cloud.biglake.v1beta.IcebergCatalogService.GetIcebergNamespace`
  - `google.cloud.biglake.v1beta.IcebergCatalogService.GetIcebergTable`
  - `google.cloud.biglake.v1beta.IcebergCatalogService.ListIcebergCatalogs`
  - `google.cloud.biglake.v1beta.IcebergCatalogService.ListIcebergNamespaces`
  - `google.cloud.biglake.v1beta.IcebergCatalogService.ListIcebergTableIdentifiers`
  - `google.cloud.biglake.v1beta.IcebergCatalogService.LoadIcebergTableCredentials`
  - `google.cloud.biglake.v1beta.IcebergCatalogService.RegisterIcebergTable`
  - `google.cloud.biglake.v1beta.IcebergCatalogService.ReportIcebergTableMetrics`
