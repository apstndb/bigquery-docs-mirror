---
name: documents/docs.cloud.google.com/bigquery/docs/introduction-audit-workloads
uri: https://docs.cloud.google.com/bigquery/docs/introduction-audit-workloads
title: Introduction to audit logs in BigQuery
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

# Introduction to audit logs in BigQuery

You can use BigQuery audit logs to monitor administrative and data access activities in your projects. Logs are text files that are automatically created and record who performed specific actions, like creating tables or running jobs, to help you maintain security and ensure compliance. This document explains when to use audit logs and provides an overview of their format.

Google Cloud also writes logs, including audit logs that provide insight into operational concerns related to your use of Google Cloud services. For more information about how Google Cloud handles logging, see the [Cloud Logging](https://docs.cloud.google.com/logging/docs) documentation and [Cloud Audit Logs overview](https://docs.cloud.google.com/logging/docs/audit) .

## Audit logs versus `INFORMATION_SCHEMA` views

Your Google Cloud projects contain audit logs only for the resources that are directly within the Google Cloud project. Other Google Cloud resources, such as folders, organizations, and billing accounts, contain their own audit logs.

Audit logs help you answer the question "Who did what, where, and when?" within your Google Cloud resources. Audit logs are the definitive source of information for system activity by user and access patterns and should be your primary source for audit or security questions.

[`INFORMATION_SCHEMA`](https://docs.cloud.google.com/bigquery/docs/information-schema-intro) views in BigQuery are another source of insights that you can use along with metrics and logs. These views contain metadata about jobs, datasets, tables, and other BigQuery entities. For example, you can get real-time metadata about which BigQuery jobs ran during a specified time. Then, you can group or filter the results by project, user, tables referenced, and other dimensions.

`INFORMATION_SCHEMA` views provide you information to perform a more detailed analysis about your BigQuery workloads, such as the following:

- What is the average slot utilization for all queries over the past seven days for a given project?
- What streaming errors occurred in the past 30 minutes, grouped by error code?

BigQuery audit logs contain log entries for API calls, but they don't describe the impact of the API calls. A subset of API calls creates jobs (such as query and load) whose information is captured by `INFORMATION_SCHEMA` views. For example, you can find information about the time and slots that are utilized by a specific query in `INFORMATION_SCHEMA` views but not in the audit logs.

To get insights into the performance of your BigQuery workloads in particular, see [jobs metadata](https://docs.cloud.google.com/bigquery/docs/information-schema-jobs) , [streaming metadata](https://docs.cloud.google.com/bigquery/docs/information-schema-streaming) , and [reservations metadata](https://docs.cloud.google.com/bigquery/docs/information-schema-reservations) .

For more information about the types of audit logs that Google Cloud services write, see [Types of audit logs](https://docs.cloud.google.com/logging/docs/audit#types) .

## Audit log format

Google Cloud services write audit logs in a structured JSON format. The base data type for Google Cloud log entries is the [`LogEntry`](https://docs.cloud.google.com/logging/docs/reference/v2/rest/v2/LogEntry) structure. This structure contains the name of the log, the resource that generated the log entry, the timestamp (UTC), and other basic information.

Logs include details of the logged event in a subfield that's called the *payload field* . For audit logs, the payload field is named `protoPayload` . This field's type ( `protoPayload.@type` ) is set to `type.googleapis.com/google.cloud.audit.AuditLog` , which indicates that the field uses the [`AuditLog`](https://docs.cloud.google.com/logging/docs/reference/audit/auditlog/rest/Shared.Types/AuditLog) log structure.

For operations on datasets, tables, and jobs, BigQuery writes audit logs in two different formats, although both formats share the `AuditLog` base type.

The older format includes the following fields and values:

- The value for the `resource.type` field is `bigquery_resource` .
- BigQuery writes the details about an operation in the `protoPayload.serviceData` field. The value of this field uses the [`AuditData`](https://docs.cloud.google.com/bigquery/docs/reference/auditlogs/rest/Shared.Types/AuditData) log structure.

The newer format includes the following fields and values:

- The value for the `resource.type` field is either `bigquery_project` or `bigquery_dataset` . The `bigquery_project` resource has log entries about jobs, while the `bigquery_dataset` resource has log entries about storage.
- BigQuery writes the details about an operation in the `protoPayload.metadata` field. The value of this field uses the [`BigQueryAuditMetadata`](https://docs.cloud.google.com/bigquery/docs/reference/auditlogs/rest/Shared.Types/BigQueryAuditMetadata) structure.

We recommend consuming logs in the newer format. For more information, see [Audit logs migration guide](https://docs.cloud.google.com/bigquery/docs/reference/auditlogs/migration) .

The following is an abbreviated example of a log entry that shows a failed operation:

```
{
  "protoPayload": {
    "@type": "type.googleapis.com/google.cloud.audit.AuditLog",
    "status": {
      "code": 5,
      "message": "Not found: Dataset myproject:mydataset was not found in location US"
    },
    "authenticationInfo": { ... },
    "requestMetadata":  { ... },
    "serviceName": "bigquery.googleapis.com",
    "methodName": "google.cloud.bigquery.v2.JobService.InsertJob",
    "metadata": {
  },
  "resource": {
    "type": "bigquery_project",
    "labels": { .. },
  },
  "severity": "ERROR",
  "logName": "projects/myproject/logs/cloudaudit.googleapis.com%2Fdata_access",
  ...
}
```

For operations on BigQuery reservations, the `protoPayload` field uses the `AuditLog` structure, and the `protoPayload.request` and `protoPayload.response` fields contain more information. You can find the field definitions in [BigQuery Reservation API](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rpc) . For more information, see [Monitoring BigQuery reservations](https://docs.cloud.google.com/bigquery/docs/reservations-monitoring) .

For a deeper understanding of the audit log format, see [Understand audit logs](https://docs.cloud.google.com/logging/docs/audit/understanding-audit-logs) .

## Limitations

Log messages have a size limit of 100,000 bytes. For more information, see [Truncated log entry](https://docs.cloud.google.com/bigquery/docs/reference/auditlogs#truncated_log_entry) .

## Visibility and access control

BigQuery audit logs can include information that users might consider sensitive, such as SQL text, schema definitions, and identifiers for resources such as tables and datasets. For information about managing access to this information, see the Cloud Logging [access control documentation](https://docs.cloud.google.com/logging/docs/access-control) .

## Telemetry map

The following table maps BigQuery features and resources to their operational monitoring telemetry, audited API services and resources, and audit log reference documentation. You can use it to find the telemetry that you need to troubleshoot issues, optimize performance, control costs, audit usage, and maintain compliance.

Unlike many Google Cloud services that write operational job logs to [Cloud Logging](https://docs.cloud.google.com/logging/docs) , BigQuery writes operational job telemetry to [information schema views](https://docs.cloud.google.com/bigquery/docs/information-schema-intro) such as [`INFORMATION_SCHEMA.JOBS`](https://docs.cloud.google.com/bigquery/docs/information-schema-jobs) . These views capture query execution stages, slot usage, bytes billed, and all submitted jobs, including in-flight and failed jobs.

BigQuery uses Logging primarily to emit [Cloud Audit Logs](https://docs.cloud.google.com/logging/docs/audit) , which record administrative and data access activity. When you audit this activity, you can determine who accessed resources or data, where, and when.

Audit logs aren't emitted for every job disruption or failure. For example, failed jobs don't generate `TableDataRead` or `TableDataChange` events, and `jobCompletedEvent` only records successful job completions. For details about scenarios that don't emit audit logs, see [Data access](https://docs.cloud.google.com/bigquery/docs/reference/auditlogs#data_access) in the [BigQuery audit logs overview](https://docs.cloud.google.com/bigquery/docs/reference/auditlogs) .

In the following table, an asterisk ( `*` ) in an `INFORMATION_SCHEMA` view name indicates scope-specific view variants, such as `_BY_PROJECT` , `_BY_USER` , `_BY_FOLDER` , and `_BY_ORGANIZATION` .

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Feature or resource</th>
<th>Operational monitoring</th>
<th>Cloud Audit Logs</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<th>Queries and jobs</th>
<td><p><strong>Information schema views:</strong></p>
<ul>
<li><a href="https://docs.cloud.google.com/bigquery/docs/information-schema-jobs"><code>JOBS*</code></a> : real-time and historical job execution, slot milliseconds, bytes billed, execution stages, and all submitted jobs regardless of completion status</li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/information-schema-jobs-timeline"><code>JOBS_ TIMELINE*</code></a> : per-timeslice job state and slot usage</li>
</ul>
<p><strong>Console:</strong></p>
<ul>
<li><a href="https://docs.cloud.google.com/bigquery/docs/admin-jobs-explorer">Jobs explorer</a> in the Google Cloud console</li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/admin-resource-charts">Administrative resource charts</a></li>
</ul>
<p><strong>Metrics:</strong> <a href="https://docs.cloud.google.com/monitoring/api/metrics_gcp_a_b#gcp-bigquery">Cloud Monitoring metrics</a> , such as <code>query/count</code> , <code>query/ execution_times</code> , and <code>job/ num_in_flight</code> .</p></td>
<td><p><strong>API service:</strong> <code>bigquery .googleapis.com</code> .</p>
<p><strong>Audited resources:</strong> jobs in <code>JobService</code> (monitored resource: <code>bigquery_project</code> ).</p>
<p><strong>Audit logs:</strong> Data Access logs using <a href="https://docs.cloud.google.com/bigquery/docs/reference/auditlogs/rest/Shared.Types/BigQueryAuditMetadata"><code>BigQuery AuditMetadata</code></a> ( <code>JobInsertion</code> and <code>JobChange</code> events), recording who submitted or canceled a job, job status, statement type, and referenced tables or views. See <a href="https://docs.cloud.google.com/bigquery/docs/reference/auditlogs#data_access">BigQuery audit logs overview</a> .</p></td>
</tr>
<tr class="even">
<th>Tables and views</th>
<td><p><strong>Information schema views:</strong></p>
<ul>
<li><a href="https://docs.cloud.google.com/bigquery/docs/information-schema-tables"><code>TABLES</code></a> : table metadata</li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/information-schema-views"><code>VIEWS</code></a> : view definitions and metadata</li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/information-schema-table-storage"><code>TABLE_ STORAGE*</code></a> : logical and physical bytes and storage billing</li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/information-schema-partitions"><code>PARTITIONS</code></a> : partition row counts and storage size</li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/information-schema-streaming"><code>STREAMING_ TIMELINE*</code></a> : streaming insert throughput and errors</li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/information-schema-write-api"><code>WRITE_API_ TIMELINE*</code></a> : write stream throughput and errors</li>
</ul>
<p><strong>Metrics:</strong> <a href="https://docs.cloud.google.com/monitoring/api/metrics_gcp_a_b#gcp-bigquery">Monitoring metrics</a> , such as <code>storage/ stored_bytes</code> and <code>storage/ table_count</code> .</p></td>
<td><p><strong>API services:</strong> <code>bigquery .googleapis.com</code> and <code>bigquerystorage .googleapis.com</code> . Data Access logs for BigQuery Storage API use <code>bigquery .googleapis.com</code> , while Policy Denied logs use <code>bigquerystorage .googleapis.com</code> .</p>
<p><strong>Audited resources:</strong> tables, views, and materialized views in <code>TableService</code> and <code>TableDataService</code> ; and storage read sessions and write streams in <code>BigQueryRead</code> and <code>BigQueryWrite</code> (monitored resources: <code>bigquery_dataset</code> and <code>bigquery_table</code> ).</p>
<p><strong>Audit logs:</strong> Data Access logs using <code>BigQuery AuditMetadata</code> ( <code>TableDataRead</code> and <code>TableDataChange</code> events for table reads, modifications, referenced fields, source job, and BigQuery Storage API stream reads and writes), plus Admin Activity, Data Access, and System Event logs for <code>TableCreation</code> , <code>TableChange</code> , and <code>TableDeletion</code> events, including table Identity and Access Management (IAM) policy changes and table expirations. See <a href="https://docs.cloud.google.com/bigquery/docs/reference/auditlogs">BigQuery audit logs overview</a> .</p></td>
</tr>
<tr class="odd">
<th>Datasets</th>
<td><p><strong>Information schema views:</strong></p>
<ul>
<li><a href="https://docs.cloud.google.com/bigquery/docs/information-schema-datasets-schemata"><code>SCHEMATA</code></a> : dataset metadata and default expiration</li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/information-schema-datasets-schemata-options"><code>SCHEMATA_ OPTIONS</code></a> : dataset options and labels</li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/information-schema-schemata-replicas"><code>SCHEMATA_ REPLICAS</code></a> : cross-region replication status</li>
</ul></td>
<td><p><strong>API service:</strong> <code>bigquery .googleapis.com</code> .</p>
<p><strong>Audited resources:</strong> datasets, dataset IAM policies, and dataset ACLs in <code>DatasetService</code> and <code>IAMPolicy</code> (monitored resource: <code>bigquery_dataset</code> ).</p>
<p><strong>Audit logs:</strong> Admin Activity and Data Access logs using <code>BigQuery AuditMetadata</code> ( <code>DatasetCreation</code> , <code>DatasetChange</code> , and <code>DatasetDeletion</code> events), including dataset IAM policy changes in <code>bindingDeltas</code> and ACL updates in <code>accessChanges</code> . See <a href="https://docs.cloud.google.com/bigquery/docs/reference/auditlogs">BigQuery audit logs overview</a> .</p></td>
</tr>
<tr class="even">
<th>Slots and reservations</th>
<td><p><strong>Information schema views:</strong></p>
<ul>
<li><a href="https://docs.cloud.google.com/bigquery/docs/information-schema-reservations"><code>RESERVATIONS*</code></a> : current reservation configurations</li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/information-schema-reservation-timeline"><code>RESERVATIONS_ TIMELINE*</code></a> : per-minute reservation metadata and autoscale details</li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/information-schema-assignments"><code>ASSIGNMENTS*</code></a> : project, folder, and organization assignments</li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/information-schema-capacity-commitments"><code>CAPACITY_ COMMITMENTS*</code></a> : slot capacity commitments</li>
</ul>
<p><strong>Console:</strong></p>
<ul>
<li><a href="https://docs.cloud.google.com/bigquery/docs/admin-resource-charts">Administrative resource charts</a> in the Google Cloud console</li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/slot-estimator">Slot estimator</a></li>
</ul>
<p><strong>Metrics:</strong> <a href="https://docs.cloud.google.com/bigquery/docs/reservations-monitoring">Monitoring metrics</a> , such as <code>slots/ allocated</code> and <code>slots/ total_available</code> .</p></td>
<td><p><strong>API service:</strong> <code>bigqueryreservation .googleapis.com</code> for the BigQuery Reservation API.</p>
<p><strong>Audited resources:</strong> reservations, capacity commitments, and reservation assignments in <code>Reservation Service</code> (monitored resource: <code>bigquery_project</code> ).</p>
<p><strong>Audit logs:</strong> Admin Activity and Data Access logs for creating, modifying, deleting, and listing reservations, capacity commitments, and project or folder assignments. See <a href="https://docs.cloud.google.com/bigquery/docs/reference/auditlogs/index-reservation">BigQuery Reservation API audit logging</a> .</p></td>
</tr>
<tr class="odd">
<th>Column-level security and data masking</th>
<td><p><strong>Information schema views:</strong></p>
<ul>
<li><a href="https://docs.cloud.google.com/bigquery/docs/information-schema-column-field-paths"><code>COLUMN_ FIELD_PATHS</code></a> : nested column paths, policy tags, and data policy assignments</li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/information-schema-columns"><code>COLUMNS</code></a> : column schemas and data types</li>
</ul></td>
<td><p><strong>API services:</strong> <code>datacatalog .googleapis.com</code> for Data Catalog policy tags, <code>bigquerydatapolicy .googleapis.com</code> for the BigQuery Data Policy API, and <code>bigquery .googleapis.com</code> .</p>
<p><strong>Audited resources:</strong> taxonomies and policy tags in <code>PolicyTagManager</code> , data policies in <code>DataPolicyService</code> , and policy-tagged table columns (monitored resources: <code>audited_resource</code> and <code>bigquery_dataset</code> ).</p>
<p><strong>Audit logs:</strong> Admin Activity and Data Access logs for taxonomy and policy tag management and IAM policy changes ( <a href="https://docs.cloud.google.com/bigquery/docs/auditing-policy-tags">Audit policy tags</a> ); data policy management and grantee updates ( <a href="https://docs.cloud.google.com/bigquery/docs/column-data-masking-audit-logging">BigQuery Data Policy audit logging</a> ); and <code>TableDataRead .fields</code> logs for reads on protected columns ( <a href="https://docs.cloud.google.com/bigquery/docs/reference/auditlogs">BigQuery audit logs overview</a> ).</p></td>
</tr>
<tr class="even">
<th>Routines, including UDFs and stored procedures</th>
<td><p><strong>Information schema views:</strong></p>
<ul>
<li><a href="https://docs.cloud.google.com/bigquery/docs/information-schema-routines"><code>ROUTINES</code></a> : routine definitions and metadata</li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/information-schema-routine-options"><code>ROUTINE_ OPTIONS</code></a> : routine options</li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/information-schema-parameters"><code>PARAMETERS</code></a> : routine input and output parameters</li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/information-schema-jobs"><code>JOBS*</code></a> : routine execution jobs</li>
</ul></td>
<td><p><strong>API service:</strong> <code>bigquery .googleapis.com</code> .</p>
<p><strong>Audited resources:</strong> user-defined functions (UDFs), table functions, and stored procedures in <code>RoutineService</code> (monitored resources: <code>bigquery_dataset</code> and <code>bigquery_project</code> ).</p>
<p><strong>Audit logs:</strong> Admin Activity and Data Access logs using <code>BigQuery AuditMetadata</code> ( <code>RoutineCreation</code> , <code>RoutineChange</code> , and <code>RoutineDeletion</code> events), plus child job events for stored procedure runs. See <a href="https://docs.cloud.google.com/bigquery/docs/reference/auditlogs">BigQuery audit logs overview</a> .</p></td>
</tr>
<tr class="odd">
<th>External connections</th>
<td><p><strong>Information schema views:</strong></p>
<ul>
<li><a href="https://docs.cloud.google.com/bigquery/docs/information-schema-object-privileges"><code>OBJECT_ PRIVILEGES</code></a> : connection privileges</li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/information-schema-jobs"><code>JOBS*</code></a> : federated queries and remote function jobs that use connections</li>
</ul></td>
<td><p><strong>API service:</strong> <code>bigqueryconnection .googleapis.com</code> for the BigQuery Connection API.</p>
<p><strong>Audited resources:</strong> connections and connection IAM policies in <code>Connection Service</code> (monitored resource: <code>audited_resource</code> ).</p>
<p><strong>Audit logs:</strong> Admin Activity and Data Access logs for connection creation, credential updates, deletion, listing, and IAM policy changes. See <a href="https://docs.cloud.google.com/bigquery/docs/reference/auditlogs/index-connection">BigQuery Connection API audit logging</a> .</p></td>
</tr>
<tr class="even">
<th>BigQuery sharing</th>
<td><p><strong>Information schema views:</strong></p>
<ul>
<li><a href="https://docs.cloud.google.com/bigquery/docs/information-schema-shared-dataset-usage"><code>SHARED_ DATASET_ USAGE</code></a> : subscriber usage of shared dataset tables</li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/information-schema-datasets-schemata-links"><code>SCHEMATA_ LINKS</code></a> : linked datasets and shared resources</li>
</ul>
<p><strong>Dashboard:</strong> <a href="https://docs.cloud.google.com/bigquery/docs/analytics-hub-monitor-listings">sharing usage metrics dashboard</a> .</p></td>
<td><p><strong>API service:</strong> <code>analyticshub .googleapis.com</code> .</p>
<p><strong>Audited resources:</strong> data exchanges, listings, subscriptions, and exchange or listing IAM policies in <code>AnalyticsHub Service</code> (monitored resource: <code>audited_resource</code> ).</p>
<p><strong>Audit logs:</strong> Admin Activity and Data Access logs for data exchange and listing creation, updates, deletion, IAM policy changes, and subscriber operations. See <a href="https://docs.cloud.google.com/bigquery/docs/analytics-hub-audit-logging">Sharing audit logging</a> .</p></td>
</tr>
<tr class="odd">
<th>BigQuery Data Transfer Service</th>
<td><p><strong>Metrics and logs:</strong></p>
<ul>
<li><a href="https://docs.cloud.google.com/bigquery/docs/dts-monitor">Monitoring transfer metrics</a></li>
<li>Operational transfer run logs in Logging under <code>resource.type= "bigquery_dts_config"</code></li>
</ul></td>
<td><p><strong>API service:</strong> <code>bigquerydatatransfer .googleapis.com</code> for the BigQuery Data Transfer Service API.</p>
<p><strong>Audited resources:</strong> transfer configurations, transfer runs, and data sources in <code>DataTransfer Service</code> (monitored resource: <code>audited_resource</code> ).</p>
<p><strong>Audit logs:</strong> Admin Activity and Data Access logs for creating, updating, deleting, listing, and starting transfer configurations and runs. See <a href="https://docs.cloud.google.com/bigquery/docs/audit-logging">BigQuery Data Transfer Service audit logging</a> .</p></td>
</tr>
<tr class="even">
<th>BigLake catalogs and tables</th>
<td><p><strong>Information schema views:</strong></p>
<ul>
<li><a href="https://docs.cloud.google.com/bigquery/docs/information-schema-tables"><code>TABLES</code></a> : table metadata</li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/information-schema-jobs"><code>JOBS*</code></a> : external object storage query statistics ( <code>metadata_cache_ statistics</code> and <code>object_storage_ stats</code> )</li>
</ul></td>
<td><p><strong>API services:</strong> <code>biglake .googleapis.com</code> and <code>bigquery .googleapis.com</code> .</p>
<p><strong>Audited resources:</strong> metastore catalogs, databases, tables, and partitions in <code>MetastoreService</code> and <code>HiveMetastore Service</code> , and Apache Iceberg catalogs, namespaces, and tables in <code>IcebergCatalog Service</code> (monitored resources: <code>audited_resource</code> and <code>bigquery_dataset</code> ).</p>
<p><strong>Audit logs:</strong> Admin Activity and Data Access logs for catalog, database, namespace, table, partition, and catalog IAM policy operations. See <a href="https://docs.cloud.google.com/bigquery/docs/biglake-audit-logging">BigLake audit logging</a> .</p></td>
</tr>
<tr class="odd">
<th>BigQuery Migration Service</th>
<td><p><strong>Status and reports:</strong></p>
<ul>
<li><a href="https://docs.cloud.google.com/bigquery/docs/batch-sql-translator">Batch SQL translation</a> job status in the Google Cloud console</li>
<li>Workflow and subtask status in the BigQuery Migration API</li>
<li>Translation summary reports in Cloud Storage</li>
</ul></td>
<td><p><strong>API service:</strong> <code>bigquerymigration .googleapis.com</code> for the BigQuery Migration API.</p>
<p><strong>Audited resources:</strong> migration workflows, migration subtasks, and SQL translation requests in <code>MigrationService</code> and <code>SqlTranslation Service</code> (monitored resource: <code>audited_resource</code> ).</p>
<p><strong>Audit logs:</strong> Data Access logs for creating, starting, listing, viewing, and deleting migration workflows and subtasks, and translating SQL queries. See <a href="https://docs.cloud.google.com/bigquery/docs/reference/auditlogs/audit-logging-bq-migration">BigQuery Migration Service audit logging</a> .</p></td>
</tr>
</tbody>
</table>

## What's next

- To learn how to use Cloud Logging to audit activities that are related to policy tags, see [Audit policy tags](https://docs.cloud.google.com/bigquery/docs/auditing-policy-tags) .
- To learn how to use BigQuery to analyze logged activity, see [BigQuery audit logs overview](https://docs.cloud.google.com/bigquery/docs/reference/auditlogs) .
