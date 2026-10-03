---
name: documents/docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info
uri: https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info
title: 'MCP Tools Reference: bigquery.googleapis.com'
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

## Tool: `get_table_info`

Get metadata information about a BigQuery table or BigLake table.

The following code sample shows how to use `curl` to call the `get_table_info` MCP tool.

**Curl Request**

```
curl --location 'https://bigquery.googleapis.com/mcp' \
--header 'content-type: application/json' \
--header 'accept: application/json, text/event-stream' \
--data '{
  "method": "tools/call",
  "params": {
    "name": "get_table_info",
    "arguments": {
      // Provide these details according to the MCP tool specification.
    }
  },
  "jsonrpc": "2.0",
  "id": 1
}'
```

## Input Schema

Request for a table.

### GetTableRequest

**JSON representation**

```
{
  "projectId": string,
  "datasetId": string,
  "tableId": string
}
```

| Fields      |                                                     |
|-------------|-----------------------------------------------------|
| `projectId` | `string` Required. Project ID of the table request. |
| `datasetId` | `string` Required. Dataset ID of the table request. |
| `tableId`   | `string` Required. Table ID of the table request.   |

## Output Schema

### Table

**JSON representation**

```
{
  "kind": string,
  "etag": string,
  "id": string,
  "selfLink": string,
  "tableReference": {
    object (TableReference)
  },
  "friendlyName": string,
  "description": string,
  "labels": {
    string: string,
    ...
  },
  "schema": {
    object (TableSchema)
  },
  "timePartitioning": {
    object (TimePartitioning)
  },
  "rangePartitioning": {
    object (RangePartitioning)
  },
  "clustering": {
    object (Clustering)
  },
  "requirePartitionFilter": boolean,
  "numBytes": string,
  "numPhysicalBytes": string,
  "numLongTermBytes": string,
  "numRows": string,
  "creationTime": string,
  "expirationTime": string,
  "lastModifiedTime": string,
  "type": string,
  "view": {
    object (ViewDefinition)
  },
  "materializedView": {
    object (MaterializedViewDefinition)
  },
  "materializedViewStatus": {
    object (MaterializedViewStatus)
  },
  "externalDataConfiguration": {
    object (ExternalDataConfiguration)
  },
  "biglakeConfiguration": {
    object (BigLakeConfiguration)
  },
  "managedTableType": enum (ManagedTableType),
  "location": string,
  "streamingBuffer": {
    object (Streamingbuffer)
  },
  "encryptionConfiguration": {
    object (EncryptionConfiguration)
  },
  "snapshotDefinition": {
    object (SnapshotDefinition)
  },
  "defaultCollation": string,
  "defaultRoundingMode": enum (RoundingMode),
  "cloneDefinition": {
    object (CloneDefinition)
  },
  "numTimeTravelPhysicalBytes": string,
  "numTotalLogicalBytes": string,
  "numActiveLogicalBytes": string,
  "numLongTermLogicalBytes": string,
  "numCurrentPhysicalBytes": string,
  "numTotalPhysicalBytes": string,
  "numActivePhysicalBytes": string,
  "numLongTermPhysicalBytes": string,
  "numPartitions": string,
  "maxStaleness": string,
  "restrictions": {
    object (RestrictionConfig)
  },
  "tableConstraints": {
    object (TableConstraints)
  },
  "resourceTags": {
    string: string,
    ...
  },
  "tableReplicationInfo": {
    object (TableReplicationInfo)
  },
  "replicas": [
    {
      object (TableReference)
    }
  ],
  "externalCatalogTableOptions": {
    object (ExternalCatalogTableOptions)
  },

  // Union field _partition_definition can be only one of the following:
  "partitionDefinition": {
    object (PartitioningDefinition)
  }
  // End of list of possible types for union field _partition_definition.
}
```

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
<td><code>kind</code></td>
<td><p><code>string</code></p>
<p>The type of resource ID.</p></td>
</tr>
<tr class="even">
<td><code>etag</code></td>
<td><p><code>string</code></p>
<p>Output only. A hash of this resource.</p></td>
</tr>
<tr class="odd">
<td><code>id</code></td>
<td><p><code>string</code></p>
<p>Output only. An opaque ID uniquely identifying the table.</p></td>
</tr>
<tr class="even">
<td><code>selfLink</code></td>
<td><p><code>string</code></p>
<p>Output only. A URL that can be used to access this resource again.</p></td>
</tr>
<tr class="odd">
<td><code>tableReference</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_dataset_info#Output.Schema.TableReference"><code>TableReference</code></a><code> )</code></p>
<p>Required. Reference describing the ID of this table.</p></td>
</tr>
<tr class="even">
<td><code>friendlyName</code></td>
<td><p><code>string</code></p>
<p>Optional. A descriptive name for this table.</p></td>
</tr>
<tr class="odd">
<td><code>description</code></td>
<td><p><code>string</code></p>
<p>Optional. A user-friendly description of this table.</p></td>
</tr>
<tr class="even">
<td><code>labels</code></td>
<td><p><code>map (key: string, value: string)</code></p>
<p>The labels associated with this table. You can use these to organize and group your tables. Label keys and values can be no longer than 63 characters, can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. Label values are optional. Label keys must start with a letter and each label in the list must have a different key.</p>
<p>An object containing a list of <code>"key": value</code> pairs. Example: <code>{ "name": "wrench", "mass": "1.3kg", "count": "3" }</code> .</p></td>
</tr>
<tr class="odd">
<td><code>schema</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.TableSchema"><code>TableSchema</code></a><code> )</code></p>
<p>Optional. Describes the schema of this table.</p></td>
</tr>
<tr class="even">
<td><code>timePartitioning</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.TimePartitioning"><code>TimePartitioning</code></a><code> )</code></p>
<p>If specified, configures time-based partitioning for this table.</p></td>
</tr>
<tr class="odd">
<td><code>rangePartitioning</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.RangePartitioning"><code>RangePartitioning</code></a><code> )</code></p>
<p>If specified, configures range partitioning for this table.</p></td>
</tr>
<tr class="even">
<td><code>clustering</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.Clustering"><code>Clustering</code></a><code> )</code></p>
<p>Clustering specification for the table. Must be specified with time-based partitioning, data in the table will be first partitioned and subsequently clustered.</p></td>
</tr>
<tr class="odd">
<td><code>requirePartitionFilter</code></td>
<td><p><code>boolean</code></p>
<p>Optional. If set to true, queries over this table require a partition filter that can be used for partition elimination to be specified.</p></td>
</tr>
<tr class="even">
<td><code>numBytes</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>Int64Value</code></a><code> format)</code></p>
<p>Output only. The size of this table in logical bytes, excluding any data in the streaming buffer.</p></td>
</tr>
<tr class="odd">
<td><code>numPhysicalBytes</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>Int64Value</code></a><code> format)</code></p>
<p>Output only. The physical size of this table in bytes. This includes storage used for time travel.</p></td>
</tr>
<tr class="even">
<td><code>numLongTermBytes</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>Int64Value</code></a><code> format)</code></p>
<p>Output only. The number of logical bytes in the table that are considered "long-term storage".</p></td>
</tr>
<tr class="odd">
<td><code>numRows</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>UInt64Value</code></a><code> format)</code></p>
<p>Output only. The number of rows of data in this table, excluding any data in the streaming buffer.</p></td>
</tr>
<tr class="even">
<td><code>creationTime</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>int64</code></a><code> format)</code></p>
<p>Output only. The time when this table was created, in milliseconds since the epoch.</p></td>
</tr>
<tr class="odd">
<td><code>expirationTime</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>Int64Value</code></a><code> format)</code></p>
<p>Optional. The time when this table expires, in milliseconds since the epoch. If not present, the table will persist indefinitely. Expired tables will be deleted and their storage reclaimed. The defaultTableExpirationMs property of the encapsulating dataset can be used to set a default expirationTime on newly created tables.</p></td>
</tr>
<tr class="even">
<td><code>lastModifiedTime</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>uint64</code></a><code> format)</code></p>
<p>Output only. The time when this table was last modified, in milliseconds since the epoch.</p></td>
</tr>
<tr class="odd">
<td><code>type</code></td>
<td><p><code>string</code></p>
<p>Output only. Describes the table type. The following values are supported:</p>
<ul>
<li><code>TABLE</code> : A normal BigQuery table.</li>
<li><code>VIEW</code> : A virtual table defined by a SQL query.</li>
<li><code>EXTERNAL</code> : A table that references data stored in an external storage system, such as Google Cloud Storage.</li>
<li><code>MATERIALIZED_VIEW</code> : A precomputed view defined by a SQL query.</li>
<li><code>SNAPSHOT</code> : An immutable BigQuery table that preserves the contents of a base table at a particular time. See additional information on <a href="https://cloud.google.com/bigquery/docs/table-snapshots-intro">table snapshots</a> .</li>
</ul>
<p>The default value is <code>TABLE</code> .</p></td>
</tr>
<tr class="even">
<td><code>view</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.ViewDefinition"><code>ViewDefinition</code></a><code> )</code></p>
<p>Optional. The view definition.</p></td>
</tr>
<tr class="odd">
<td><code>materializedView</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.MaterializedViewDefinition"><code>MaterializedViewDefinition</code></a><code> )</code></p>
<p>Optional. The materialized view definition.</p></td>
</tr>
<tr class="even">
<td><code>materializedViewStatus</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.MaterializedViewStatus"><code>MaterializedViewStatus</code></a><code> )</code></p>
<p>Output only. The materialized view status.</p></td>
</tr>
<tr class="odd">
<td><code>externalDataConfiguration</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.ExternalDataConfiguration"><code>ExternalDataConfiguration</code></a><code> )</code></p>
<p>Optional. Describes the data format, location, and other properties of a table stored outside of BigQuery. By defining these properties, the data source can then be queried as if it were a standard BigQuery table.</p></td>
</tr>
<tr class="even">
<td><code>biglakeConfiguration</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.BigLakeConfiguration"><code>BigLakeConfiguration</code></a><code> )</code></p>
<p>Optional. Specifies the configuration of a BigQuery table for Apache Iceberg.</p></td>
</tr>
<tr class="odd">
<td><code>managedTableType</code></td>
<td><p><code>enum ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.ManagedTableType"><code>ManagedTableType</code></a><code> )</code></p>
<p>Optional. If set, overrides the default managed table type configured in the dataset.</p></td>
</tr>
<tr class="even">
<td><code>location</code></td>
<td><p><code>string</code></p>
<p>Output only. The geographic location where the table resides. This value is inherited from the dataset.</p></td>
</tr>
<tr class="odd">
<td><code>streamingBuffer</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.Streamingbuffer"><code>Streamingbuffer</code></a><code> )</code></p>
<p>Output only. Contains information regarding this table's streaming buffer, if one is present. This field will be absent if the table is not being streamed to or if there is no data in the streaming buffer.</p></td>
</tr>
<tr class="even">
<td><code>encryptionConfiguration</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_dataset_info#Output.Schema.EncryptionConfiguration"><code>EncryptionConfiguration</code></a><code> )</code></p>
<p>Custom encryption configuration (e.g., Cloud KMS keys).</p></td>
</tr>
<tr class="odd">
<td><code>snapshotDefinition</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.SnapshotDefinition"><code>SnapshotDefinition</code></a><code> )</code></p>
<p>Output only. Contains information about the snapshot. This value is set via snapshot creation.</p></td>
</tr>
<tr class="even">
<td><code>defaultCollation</code></td>
<td><p><code>string</code></p>
<p>Optional. Defines the default collation specification of new STRING fields in the table. During table creation or update, if a STRING field is added to this table without explicit collation specified, then the table inherits the table default collation. A change to this field affects only fields added afterwards, and does not alter the existing fields. The following values are supported:</p>
<ul>
<li>'und:ci': undetermined locale, case insensitive.</li>
<li>'': empty string. Default to case-sensitive behavior.</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>defaultRoundingMode</code></td>
<td><p><code>enum ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_dataset_info#Output.Schema.RoundingMode"><code>RoundingMode</code></a><code> )</code></p>
<p>Optional. Defines the default rounding mode specification of new decimal fields (NUMERIC OR BIGNUMERIC) in the table. During table creation or update, if a decimal field is added to this table without an explicit rounding mode specified, then the field inherits the table default rounding mode. Changing this field doesn't affect existing fields.</p></td>
</tr>
<tr class="even">
<td><code>cloneDefinition</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.CloneDefinition"><code>CloneDefinition</code></a><code> )</code></p>
<p>Output only. Contains information about the clone. This value is set via the clone operation.</p></td>
</tr>
<tr class="odd">
<td><code>numTimeTravelPhysicalBytes</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>Int64Value</code></a><code> format)</code></p>
<p>Output only. Number of physical bytes used by time travel storage (deleted or changed data). This data is not kept in real time, and might be delayed by a few seconds to a few minutes.</p></td>
</tr>
<tr class="even">
<td><code>numTotalLogicalBytes</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>Int64Value</code></a><code> format)</code></p>
<p>Output only. Total number of logical bytes in the table or materialized view.</p></td>
</tr>
<tr class="odd">
<td><code>numActiveLogicalBytes</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>Int64Value</code></a><code> format)</code></p>
<p>Output only. Number of logical bytes that are less than 90 days old.</p></td>
</tr>
<tr class="even">
<td><code>numLongTermLogicalBytes</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>Int64Value</code></a><code> format)</code></p>
<p>Output only. Number of logical bytes that are more than 90 days old.</p></td>
</tr>
<tr class="odd">
<td><code>numCurrentPhysicalBytes</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>Int64Value</code></a><code> format)</code></p>
<p>Output only. Number of physical bytes used by current live data storage. This data is not kept in real time, and might be delayed by a few seconds to a few minutes.</p></td>
</tr>
<tr class="even">
<td><code>numTotalPhysicalBytes</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>Int64Value</code></a><code> format)</code></p>
<p>Output only. The physical size of this table in bytes. This also includes storage used for time travel. This data is not kept in real time, and might be delayed by a few seconds to a few minutes.</p></td>
</tr>
<tr class="odd">
<td><code>numActivePhysicalBytes</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>Int64Value</code></a><code> format)</code></p>
<p>Output only. Number of physical bytes less than 90 days old. This data is not kept in real time, and might be delayed by a few seconds to a few minutes.</p></td>
</tr>
<tr class="even">
<td><code>numLongTermPhysicalBytes</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>Int64Value</code></a><code> format)</code></p>
<p>Output only. Number of physical bytes more than 90 days old. This data is not kept in real time, and might be delayed by a few seconds to a few minutes.</p></td>
</tr>
<tr class="odd">
<td><code>numPartitions</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>Int64Value</code></a><code> format)</code></p>
<p>Output only. The number of partitions present in the table or materialized view. This data is not kept in real time, and might be delayed by a few seconds to a few minutes.</p></td>
</tr>
<tr class="even">
<td><code>maxStaleness</code></td>
<td><p><code>string</code></p>
<p>Optional. The maximum staleness of data that could be returned when the table (or stale MV) is queried. Staleness encoded as a string encoding of sql IntervalValue type.</p></td>
</tr>
<tr class="odd">
<td><code>restrictions</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_dataset_info#Output.Schema.RestrictionConfig"><code>RestrictionConfig</code></a><code> )</code></p>
<p>Optional. Output only. Restriction config for table. If set, restrict certain accesses on the table based on the config. See <a href="https://cloud.google.com/bigquery/docs/analytics-hub-introduction#data_egress">Data egress</a> for more details.</p></td>
</tr>
<tr class="even">
<td><code>tableConstraints</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.TableConstraints"><code>TableConstraints</code></a><code> )</code></p>
<p>Optional. Tables Primary Key and Foreign Key information</p></td>
</tr>
<tr class="odd">
<td><code>resourceTags</code></td>
<td><p><code>map (key: string, value: string)</code></p>
<p>Optional. The <a href="https://cloud.google.com/bigquery/docs/tags">tags</a> attached to this table. Tag keys are globally unique. Tag key is expected to be in the namespaced format, for example "123456789012/environment" where 123456789012 is the ID of the parent organization or project resource for this tag key. Tag value is expected to be the short name, for example "Production". See <a href="https://cloud.google.com/iam/docs/tags-access-control#definitions">Tag definitions</a> for more details.</p>
<p>An object containing a list of <code>"key": value</code> pairs. Example: <code>{ "name": "wrench", "mass": "1.3kg", "count": "3" }</code> .</p></td>
</tr>
<tr class="even">
<td><code>tableReplicationInfo</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.TableReplicationInfo"><code>TableReplicationInfo</code></a><code> )</code></p>
<p>Optional. Table replication info for table created <code>AS REPLICA</code> DDL like: <code>CREATE MATERIALIZED VIEW mv1 AS REPLICA OF src_mv</code></p></td>
</tr>
<tr class="odd">
<td><code>replicas[]</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_dataset_info#Output.Schema.TableReference"><code>TableReference</code></a><code> )</code></p>
<p>Optional. Output only. Table references of all replicas currently active on the table.</p></td>
</tr>
<tr class="even">
<td><code>externalCatalogTableOptions</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.ExternalCatalogTableOptions"><code>ExternalCatalogTableOptions</code></a><code> )</code></p>
<p>Optional. Options defining open source compatible table.</p></td>
</tr>
<tr class="odd">
<td><p>Union field <code>_partition_definition</code> .</p>
<p><code>_partition_definition</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="even">
<td><code>partitionDefinition</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.PartitioningDefinition"><code>PartitioningDefinition</code></a><code> )</code></p>
<p>Optional. The partition information for all table formats, including managed partitioned tables, hive partitioned tables, iceberg partitioned, and metastore partitioned tables. This field is only populated for metastore partitioned tables. For other table formats, this is an output only field.</p></td>
</tr>
<tr class="odd">
<td></td>
<td></td>
</tr>
</tbody>
</table>

### TableReference

**JSON representation**

```
{
  "projectId": string,
  "datasetId": string,
  "tableId": string
}
```

| Fields      |                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
|-------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `projectId` | `string` Required. The ID of the project containing this table.                                                                                                                                                                                                                                                                                                                                                                                                              |
| `datasetId` | `string` Required. The ID of the dataset containing this table.                                                                                                                                                                                                                                                                                                                                                                                                              |
| `tableId`   | `string` Required. The ID of the table. The ID can contain Unicode characters in category L (letter), M (mark), N (number), Pc (connector, including underscore), Pd (dash), and Zs (space). For more information, see [General Category](https://wikipedia.org/wiki/Unicode_character_property#General_Category) . The maximum length is 1,024 characters. Certain operations allow suffixing of the table ID with a partition decorator, such as `sample_table$20190123` . |

### StringValue

**JSON representation**

```
{
  "value": string
}
```

| Fields  |                            |
|---------|----------------------------|
| `value` | `string` The string value. |

### LabelsEntry

**JSON representation**

```
{
  "key": string,
  "value": string
}
```

| Fields  |          |
|---------|----------|
| `key`   | `string` |
| `value` | `string` |

### TableSchema

**JSON representation**

```
{
  "fields": [
    {
      object (TableFieldSchema)
    }
  ],
  "foreignTypeInfo": {
    object (ForeignTypeInfo)
  }
}
```

| Fields            |                                                                                                                                                                                                                                                                                        |
|-------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `fields[]`        | `object ( `[`TableFieldSchema`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.TableFieldSchema)` )` Describes the fields in a table.                                                                                               |
| `foreignTypeInfo` | `object ( `[`ForeignTypeInfo`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.ForeignTypeInfo)` )` Optional. Specifies metadata of the foreign data type definition in field schema ( `TableFieldSchema.foreign_type_definition` ). |

### TableFieldSchema

**JSON representation**

```
{
  "name": string,
  "type": string,
  "mode": string,
  "fields": [
    {
      object (TableFieldSchema)
    }
  ],
  "description": string,
  "policyTags": {
    object (PolicyTagList)
  },
  "dataGovernanceTagsInfo": {
    object (DataGovernanceTagsInfo)
  },
  "dataPolicies": [
    {
      object (DataPolicyOption)
    }
  ],
  "dataPolicyList": {
    object (DataPolicyList)
  },
  "maxLength": string,
  "precision": string,
  "scale": string,
  "timestampPrecision": string,
  "roundingMode": enum (RoundingMode),
  "collation": string,
  "defaultValueExpression": string,
  "rangeElementType": {
    object (FieldElementType)
  },
  "foreignTypeDefinition": string,
  "generatedColumn": {
    object (GeneratedColumn)
  }
}
```

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
<td><code>name</code></td>
<td><p><code>string</code></p>
<p>Required. The field name. The name must contain only letters (a-z, A-Z), numbers (0-9), or underscores (_), and must start with a letter or underscore. The maximum length is 300 characters.</p></td>
</tr>
<tr class="even">
<td><code>type</code></td>
<td><p><code>string</code></p>
<p>Required. The field data type. Possible values include:</p>
<ul>
<li>STRING</li>
<li>BYTES</li>
<li>INTEGER (or INT64)</li>
<li>FLOAT (or FLOAT64)</li>
<li>BOOLEAN (or BOOL)</li>
<li>TIMESTAMP</li>
<li>DATE</li>
<li>TIME</li>
<li>DATETIME</li>
<li>GEOGRAPHY</li>
<li>NUMERIC</li>
<li>BIGNUMERIC</li>
<li>JSON</li>
<li>RECORD (or STRUCT)</li>
<li>RANGE</li>
</ul>
<p>Use of RECORD/STRUCT indicates that the field contains a nested schema.</p></td>
</tr>
<tr class="odd">
<td><code>mode</code></td>
<td><p><code>string</code></p>
<p>Optional. The field mode. Possible values include NULLABLE, REQUIRED and REPEATED. The default value is NULLABLE.</p></td>
</tr>
<tr class="even">
<td><code>fields[]</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.TableFieldSchema"><code>TableFieldSchema</code></a><code> )</code></p>
<p>Optional. Describes the nested schema fields if the type property is set to RECORD.</p></td>
</tr>
<tr class="odd">
<td><code>description</code></td>
<td><p><code>string</code></p>
<p>Optional. The field description. The maximum length is 1,024 characters.</p></td>
</tr>
<tr class="even">
<td><code>policyTags</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.PolicyTagList"><code>PolicyTagList</code></a><code> )</code></p>
<p>Optional. The policy tags attached to this field, used for field-level access control. If not set, defaults to empty policy_tags.</p></td>
</tr>
<tr class="odd">
<td><code>dataGovernanceTagsInfo</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.DataGovernanceTagsInfo"><code>DataGovernanceTagsInfo</code></a><code> )</code></p>
<p>Optional. Specifies the data governance tags on this field. This field works with other column-level security fields as follows:</p>
<ul>
<li><strong>Precedence</strong> : If a data governance tag is attached to a column, it takes precedence over the policy tag attached to the column. However, if a data policy is attached to a column, it takes precedence over the data governance tag.</li>
<li><strong>Patching behavior</strong> : Describes how this field behaves during a <code>Table.patch</code> schema update:
<ul>
<li><strong>Unset</strong> : If the <code>data_governance_tags_info</code> field is omitted from the update request, the existing tags on the column are preserved.</li>
<li><strong>Empty Field</strong> : To clear data governance tags from a column, send the <code>data_governance_tags_info</code> field as an empty object. This removes all tags from the column.</li>
<li><strong>Updating tags</strong> : To replace an existing tag, send the field with the new tag.</li>
</ul></li>
</ul></td>
</tr>
<tr class="even">
<td><code>dataPolicies[]</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.DataPolicyOption"><code>DataPolicyOption</code></a><code> )</code></p>
<p>Optional. Data policies attached to this field, used for field-level access control.</p></td>
</tr>
<tr class="odd">
<td><code>dataPolicyList</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.DataPolicyList"><code>DataPolicyList</code></a><code> )</code></p>
<p>Optional. Specifies data policies attached to this field, used for field-level access control. When set, this will be the source of truth for data policy information.</p></td>
</tr>
<tr class="even">
<td><code>maxLength</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>int64</code></a><code> format)</code></p>
<p>Optional. Maximum length of values of this field for STRINGS or BYTES.</p>
<p>If max_length is not specified, no maximum length constraint is imposed on this field.</p>
<p>If type = "STRING", then max_length represents the maximum UTF-8 length of strings in this field.</p>
<p>If type = "BYTES", then max_length represents the maximum number of bytes in this field.</p>
<p>It is invalid to set this field if type ≠ "STRING" and ≠ "BYTES".</p></td>
</tr>
<tr class="odd">
<td><code>precision</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>int64</code></a><code> format)</code></p>
<p>Optional. Precision (maximum number of total digits in base 10) and scale (maximum number of digits in the fractional part in base 10) constraints for values of this field for NUMERIC or BIGNUMERIC.</p>
<p>It is invalid to set precision or scale if type ≠ "NUMERIC" and ≠ "BIGNUMERIC".</p>
<p>If precision and scale are not specified, no value range constraint is imposed on this field insofar as values are permitted by the type.</p>
<p>Values of this NUMERIC or BIGNUMERIC field must be in this range when:</p>
<ul>
<li>Precision ( <var translate="no"> P </var> ) and scale ( <var translate="no"> S </var> ) are specified: [-10 <sup><var translate="no"> P </var> - <var translate="no"> S </var></sup> + 10 <sup>- <var translate="no"> S </var></sup> , 10 <sup><var translate="no"> P </var> - <var translate="no"> S </var></sup> - 10 <sup>- <var translate="no"> S </var></sup> ]</li>
<li>Precision ( <var translate="no"> P </var> ) is specified but not scale (and thus scale is interpreted to be equal to zero): [-10 <sup><var translate="no"> P </var></sup> + 1, 10 <sup><var translate="no"> P </var></sup> - 1].</li>
</ul>
<p>Acceptable values for precision and scale if both are specified:</p>
<ul>
<li>If type = "NUMERIC": 1 ≤ precision - scale ≤ 29 and 0 ≤ scale ≤ 9.</li>
<li>If type = "BIGNUMERIC": 1 ≤ precision - scale ≤ 38 and 0 ≤ scale ≤ 38.</li>
</ul>
<p>Acceptable values for precision if only precision is specified but not scale (and thus scale is interpreted to be equal to zero):</p>
<ul>
<li>If type = "NUMERIC": 1 ≤ precision ≤ 29.</li>
<li>If type = "BIGNUMERIC": 1 ≤ precision ≤ 38.</li>
</ul>
<p>If scale is specified but not precision, then it is invalid.</p></td>
</tr>
<tr class="even">
<td><code>scale</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>int64</code></a><code> format)</code></p>
<p>Optional. See documentation for precision.</p></td>
</tr>
<tr class="odd">
<td><code>timestampPrecision</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>Int64Value</code></a><code> format)</code></p>
<p>Optional. Precision (maximum number of total digits in base 10) for seconds of TIMESTAMP type.</p>
<p>Possible values include: * 6 (Default, for TIMESTAMP type with microsecond precision) * 12 (For TIMESTAMP type with picosecond precision)</p></td>
</tr>
<tr class="even">
<td><code>roundingMode</code></td>
<td><p><code>enum ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_dataset_info#Output.Schema.RoundingMode"><code>RoundingMode</code></a><code> )</code></p>
<p>Optional. Specifies the rounding mode to be used when storing values of NUMERIC and BIGNUMERIC type.</p></td>
</tr>
<tr class="odd">
<td><code>collation</code></td>
<td><p><code>string</code></p>
<p>Optional. Field collation can be set only when the type of field is STRING. The following values are supported:</p>
<ul>
<li>'und:ci': undetermined locale, case insensitive.</li>
<li>'': empty string. Default to case-sensitive behavior.</li>
</ul></td>
</tr>
<tr class="even">
<td><code>defaultValueExpression</code></td>
<td><p><code>string</code></p>
<p>Optional. A SQL expression to specify the <a href="https://cloud.google.com/bigquery/docs/default-values">default value</a> for this field.</p></td>
</tr>
<tr class="odd">
<td><code>rangeElementType</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.FieldElementType"><code>FieldElementType</code></a><code> )</code></p>
<p>Optional. The subtype of the RANGE, if the type of this field is RANGE. If the type is RANGE, this field is required. Values for the field element type can be the following:</p>
<ul>
<li>DATE</li>
<li>DATETIME</li>
<li>TIMESTAMP</li>
</ul></td>
</tr>
<tr class="even">
<td><code>foreignTypeDefinition</code></td>
<td><p><code>string</code></p>
<p>Optional. Definition of the foreign data type. Only valid for top-level schema fields (not nested fields). If the type is FOREIGN, this field is required.</p></td>
</tr>
<tr class="odd">
<td><code>generatedColumn</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.GeneratedColumn"><code>GeneratedColumn</code></a><code> )</code></p>
<p>Optional. Definition of how values are generated for the field. Only valid for top-level schema fields (not nested fields).</p></td>
</tr>
</tbody>
</table>

### PolicyTagList

**JSON representation**

```
{
  "names": [
    string
  ]
}
```

| Fields    |                                                                                                                                                            |
|-----------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `names[]` | `string` A list of policy tag resource names. For example, "projects/1/locations/eu/taxonomies/2/policyTags/3". At most 1 policy tag is currently allowed. |

### DataGovernanceTagsInfo

**JSON representation**

```
{
  "dataGovernanceTags": {
    string: string,
    ...
  }
}
```

| Fields               |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
|----------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `dataGovernanceTags` | `map (key: string, value: string)` Optional. The data governance tags added to this field are used for field-level access control. Only one data governance tag is currently supported on a field. Tag keys are globally unique. Tag key is expected to be in the namespaced format, for example "parent-id/pii" where parent-id is the ID of the parent organization or project resource for this tag key. Tag value is expected to be the short name, for example "sensitive". See [Tag definitions](https://cloud.google.com/iam/docs/tags-access-control#definitions) for more details. For example: "parent-id/pii": "sensitive", "myProject/cost_center": "sales" An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` . |

### DataGovernanceTagsEntry

**JSON representation**

```
{
  "key": string,
  "value": string
}
```

| Fields  |          |
|---------|----------|
| `key`   | `string` |
| `value` | `string` |

### DataPolicyOption

**JSON representation**

```
{

  // Union field _name can be only one of the following:
  "name": string
  // End of list of possible types for union field _name.
}
```

| Fields                                                          |                                                                                                                          |
|-----------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------|
| Union field `_name` . `_name` can be only one of the following: |                                                                                                                          |
| `name`                                                          | `string` Data policy resource name in the form of projects/project_id/locations/location_id/dataPolicies/data_policy_id. |
|                                                                 |                                                                                                                          |

### DataPolicyList

**JSON representation**

```
{
  "dataPolicies": [
    {
      object (DataPolicyOption)
    }
  ]
}
```

| Fields           |                                                                                                                                                                                                                                                |
|------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `dataPolicies[]` | `object ( `[`DataPolicyOption`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.DataPolicyOption)` )` Contains a list of data policy options. At most 9 data policies are allowed per field. |

### Int64Value

**JSON representation**

```
{
  "value": string
}
```

| Fields  |                                                                                                         |
|---------|---------------------------------------------------------------------------------------------------------|
| `value` | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` The int64 value. |

### FieldElementType

**JSON representation**

```
{
  "type": string
}
```

| Fields |                                                                                                     |
|--------|-----------------------------------------------------------------------------------------------------|
| `type` | `string` Required. The type of a field element. For more information, see `TableFieldSchema.type` . |

### GeneratedColumn

**JSON representation**

```
{

  // Union field _generated_mode can be only one of the following:
  "generatedMode": enum (GeneratedMode)
  // End of list of possible types for union field _generated_mode.

  // Union field definition can be only one of the following:
  "generatedExpressionInfo": {
    object (GeneratedExpressionInfo)
  }
  // End of list of possible types for union field definition.
}
```

| Fields                                                                              |                                                                                                                                                                                                                                 |
|-------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `_generated_mode` . `_generated_mode` can be only one of the following: |                                                                                                                                                                                                                                 |
| `generatedMode`                                                                     | `enum ( `[`GeneratedMode`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.GeneratedMode)` )` Optional. Dictates when system generated values are used to populate the field. |
|                                                                                     |                                                                                                                                                                                                                                 |
| Union field `definition` . `definition` can be only one of the following:           |                                                                                                                                                                                                                                 |
| `generatedExpressionInfo`                                                           | `object ( `[`GeneratedExpressionInfo`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.GeneratedExpressionInfo)` )` Definition of the expression used to generate the field.  |
|                                                                                     |                                                                                                                                                                                                                                 |

### GeneratedExpressionInfo

**JSON representation**

```
{

  // Union field _generation_expression can be only one of the following:
  "generationExpression": string
  // End of list of possible types for union field _generation_expression.

  // Union field _asynchronous can be only one of the following:
  "asynchronous": boolean
  // End of list of possible types for union field _asynchronous.

  // Union field _stored can be only one of the following:
  "stored": boolean
  // End of list of possible types for union field _stored.
}
```

| Fields                                                                                            |                                                                                               |
|---------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------|
| Union field `_generation_expression` . `_generation_expression` can be only one of the following: |                                                                                               |
| `generationExpression`                                                                            | `string` Optional. The generation expression (e.g. AI.EMBED(...)) used to generate the field. |
|                                                                                                   |                                                                                               |
| Union field `_asynchronous` . `_asynchronous` can be only one of the following:                   |                                                                                               |
| `asynchronous`                                                                                    | `boolean` Optional. Whether the column generation is done asynchronously.                     |
|                                                                                                   |                                                                                               |
| Union field `_stored` . `_stored` can be only one of the following:                               |                                                                                               |
| `stored`                                                                                          | `boolean` Optional. Whether the generated column is stored in the table.                      |
|                                                                                                   |                                                                                               |

### ForeignTypeInfo

**JSON representation**

```
{
  "typeSystem": enum (TypeSystem)
}
```

| Fields       |                                                                                                                                                                                                               |
|--------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `typeSystem` | `enum ( `[`TypeSystem`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.TypeSystem)` )` Required. Specifies the system which defines the foreign data type. |

### TimePartitioning

**JSON representation**

```
{
  "type": string,
  "expirationMs": string,
  "field": string,
  "requirePartitionFilter": boolean
}
```

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
<td><code>type</code></td>
<td><p><code>string</code></p>
<p>Required. The supported types are DAY, HOUR, MONTH, and YEAR, which will generate one partition per day, hour, month, and year, respectively.</p></td>
</tr>
<tr class="even">
<td><code>expirationMs</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>Int64Value</code></a><code> format)</code></p>
<p>Optional. Number of milliseconds for which to keep the storage for a partition. A wrapper is used here because 0 is an invalid value.</p></td>
</tr>
<tr class="odd">
<td><code>field</code></td>
<td><p><code>string</code></p>
<p>Optional. If not set, the table is partitioned by pseudo column '_PARTITIONTIME'; if set, the table is partitioned by this field. The field must be a top-level TIMESTAMP or DATE field. Its mode must be NULLABLE or REQUIRED. A wrapper is used here because an empty string is an invalid value.</p></td>
</tr>
<tr class="even">
<td><code>requirePartitionFilter </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>boolean</code></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>If set to true, queries over this table require a partition filter that can be used for partition elimination to be specified. This field is deprecated; please set the field with the same name on the table itself instead. This field needs a wrapper because we want to output the default value, false, if the user explicitly set it.</p></td>
</tr>
</tbody>
</table>

### BoolValue

**JSON representation**

```
{
  "value": boolean
}
```

| Fields  |                           |
|---------|---------------------------|
| `value` | `boolean` The bool value. |

### RangePartitioning

**JSON representation**

```
{
  "field": string,
  "range": {
    object (Range)
  }
}
```

| Fields  |                                                                                                                                                                              |
|---------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `field` | `string` Required. The name of the column to partition the table on. It must be a top-level, INT64 column whose mode is NULLABLE or REQUIRED.                                |
| `range` | `object ( `[`Range`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.Range)` )` Defines the ranges for range partitioning. |

### Range

**JSON representation**

```
{
  "start": string,
  "end": string,
  "interval": string
}
```

| Fields     |                                                                                                                      |
|------------|----------------------------------------------------------------------------------------------------------------------|
| `start`    | `string` Required. The start of range partitioning, inclusive. This field is an INT64 value represented as a string. |
| `end`      | `string` Required. The end of range partitioning, exclusive. This field is an INT64 value represented as a string.   |
| `interval` | `string` Required. The width of each interval. This field is an INT64 value represented as a string.                 |

### Clustering

**JSON representation**

```
{
  "fields": [
    string
  ]
}
```

| Fields     |                                                                                                                                                                                                                                                                                                                                                                                           |
|------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `fields[]` | `string` One or more fields on which data should be clustered. Only top-level, non-repeated, simple-type fields are supported. The ordering of the clustering fields should be prioritized from most to least important for filtering purposes. For additional information, see [Introduction to clustered tables](https://cloud.google.com/bigquery/docs/clustered-tables#limitations) . |

### PartitioningDefinition

**JSON representation**

```
{
  "partitionedColumn": [
    {
      object (PartitionedColumn)
    }
  ]
}
```

| Fields                |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
|-----------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `partitionedColumn[]` | `object ( `[`PartitionedColumn`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.PartitionedColumn)` )` Optional. Details about each partitioning column. This field is output only for all partitioning types other than metastore partitioned tables. BigQuery native tables only support 1 partitioning column. Other table types may support 0, 1 or more partitioning columns. For metastore partitioned tables, the order must match the definition order in the Hive Metastore, where it must match the physical layout of the table. For example, CREATE TABLE a_table(id BIGINT, name STRING) PARTITIONED BY (city STRING, state STRING). In this case the values must be \['city', 'state'\] in that order. |

### PartitionedColumn

**JSON representation**

```
{

  // Union field _field can be only one of the following:
  "field": string
  // End of list of possible types for union field _field.
}
```

| Fields                                                            |                                                      |
|-------------------------------------------------------------------|------------------------------------------------------|
| Union field `_field` . `_field` can be only one of the following: |                                                      |
| `field`                                                           | `string` Required. The name of the partition column. |
|                                                                   |                                                      |

### UInt64Value

**JSON representation**

```
{
  "value": string
}
```

| Fields  |                            |
|---------|----------------------------|
| `value` | `string` The uint64 value. |

### ViewDefinition

**JSON representation**

```
{
  "query": string,
  "userDefinedFunctionResources": [
    {
      object (UserDefinedFunctionResource)
    }
  ],
  "useLegacySql": boolean,
  "useExplicitColumnNames": boolean,
  "privacyPolicy": {
    object (PrivacyPolicy)
  },
  "foreignDefinitions": [
    {
      object (ForeignViewDefinition)
    }
  ]
}
```

| Fields                           |                                                                                                                                                                                                                                                                                                                                                             |
|----------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `query`                          | `string` Required. A query that BigQuery executes when the view is referenced.                                                                                                                                                                                                                                                                              |
| `userDefinedFunctionResources[]` | `object ( `[`UserDefinedFunctionResource`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.UserDefinedFunctionResource)` )` Describes user-defined function resources used in the query.                                                                                                                  |
| `useLegacySql`                   | `boolean` Specifies whether to use BigQuery's legacy SQL for this view. The default value is true. If set to false, the view uses BigQuery's [GoogleSQL](https://docs.cloud.google.com/bigquery/docs/introduction-sql) . Queries and views that reference this view must use the same flag value. A wrapper is used here because the default value is True. |
| `useExplicitColumnNames`         | `boolean` True if the column names are explicitly specified. For example by using the 'CREATE VIEW v(c1, c2) AS ...' syntax. Can only be set for GoogleSQL views.                                                                                                                                                                                           |
| `privacyPolicy`                  | `object ( `[`PrivacyPolicy`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.PrivacyPolicy)` )` Optional. Specifies the privacy policy for the view.                                                                                                                                                      |
| `foreignDefinitions[]`           | `object ( `[`ForeignViewDefinition`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.ForeignViewDefinition)` )` Optional. Foreign view representations.                                                                                                                                                   |

### UserDefinedFunctionResource

**JSON representation**

```
{
  "resourceUri": string,
  "inlineCode": string
}
```

| Fields        |                                                                                                                                                                                                       |
|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `resourceUri` | `string` \[Pick one\] A code resource to load from a Google Cloud Storage URI (gs://bucket/path).                                                                                                     |
| `inlineCode`  | `string` \[Pick one\] An inline resource that contains code for a user-defined function (UDF). Providing a inline code resource is equivalent to providing a URI for a file containing the same code. |

### PrivacyPolicy

**JSON representation**

```
{

  // Union field privacy_policy can be only one of the following:
  "aggregationThresholdPolicy": {
    object (AggregationThresholdPolicy)
  },
  "differentialPrivacyPolicy": {
    object (DifferentialPrivacyPolicy)
  }
  // End of list of possible types for union field privacy_policy.

  // Union field _join_restriction_policy can be only one of the following:
  "joinRestrictionPolicy": {
    object (JoinRestrictionPolicy)
  }
  // End of list of possible types for union field _join_restriction_policy.
}
```

| Fields                                                                                                                                                                                                              |                                                                                                                                                                                                                                                                                                                                                                                                                                                |
|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `privacy_policy` . Privacy policy associated with this requirement specification. Only one of the privacy methods is allowed per data source object. `privacy_policy` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| `aggregationThresholdPolicy`                                                                                                                                                                                        | `object ( `[`AggregationThresholdPolicy`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.AggregationThresholdPolicy)` )` Optional. Policy used for aggregation thresholds.                                                                                                                                                                                                                  |
| `differentialPrivacyPolicy`                                                                                                                                                                                         | `object ( `[`DifferentialPrivacyPolicy`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.DifferentialPrivacyPolicy)` )` Optional. Policy used for differential privacy.                                                                                                                                                                                                                      |
|                                                                                                                                                                                                                     |                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| Union field `_join_restriction_policy` . `_join_restriction_policy` can be only one of the following:                                                                                                               |                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| `joinRestrictionPolicy`                                                                                                                                                                                             | `object ( `[`JoinRestrictionPolicy`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.JoinRestrictionPolicy)` )` Optional. Join restriction policy is outside of the one of policies, since this policy can be set along with other policies. This policy gives data providers the ability to enforce joins on the 'join_allowed_columns' when data is queried from a privacy protected view. |
|                                                                                                                                                                                                                     |                                                                                                                                                                                                                                                                                                                                                                                                                                                |

### AggregationThresholdPolicy

**JSON representation**

```
{
  "privacyUnitColumns": [
    string
  ],

  // Union field _threshold can be only one of the following:
  "threshold": string
  // End of list of possible types for union field _threshold.
}
```

| Fields                                                                    |                                                                                                                                                                                                                                                                                                                                                                                        |
|---------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `privacyUnitColumns[]`                                                    | `string` Optional. The privacy unit column(s) associated with this policy. For now, only one column per data source object (table, view) is allowed as a privacy unit column. Representing as a repeated field in metadata for extensibility to multiple columns in future. Duplicates and Repeated struct fields are not allowed. For nested fields, use dot notation ("outer.inner") |
| Union field `_threshold` . `_threshold` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                                                        |
| `threshold`                                                               | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Optional. The threshold for the "aggregation threshold" policy.                                                                                                                                                                                                                                 |
|                                                                           |                                                                                                                                                                                                                                                                                                                                                                                        |

### DifferentialPrivacyPolicy

**JSON representation**

```
{

  // Union field _max_epsilon_per_query can be only one of the following:
  "maxEpsilonPerQuery": number
  // End of list of possible types for union field _max_epsilon_per_query.

  // Union field _delta_per_query can be only one of the following:
  "deltaPerQuery": number
  // End of list of possible types for union field _delta_per_query.

  // Union field _max_groups_contributed can be only one of the following:
  "maxGroupsContributed": string
  // End of list of possible types for union field _max_groups_contributed.

  // Union field _privacy_unit_column can be only one of the following:
  "privacyUnitColumn": string
  // End of list of possible types for union field _privacy_unit_column.

  // Union field _epsilon_budget can be only one of the following:
  "epsilonBudget": number
  // End of list of possible types for union field _epsilon_budget.

  // Union field _delta_budget can be only one of the following:
  "deltaBudget": number
  // End of list of possible types for union field _delta_budget.

  // Union field _epsilon_budget_remaining can be only one of the following:
  "epsilonBudgetRemaining": number
  // End of list of possible types for union field _epsilon_budget_remaining.

  // Union field _delta_budget_remaining can be only one of the following:
  "deltaBudgetRemaining": number
  // End of list of possible types for union field _delta_budget_remaining.
}
```

| Fields                                                                                                  |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
|---------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `_max_epsilon_per_query` . `_max_epsilon_per_query` can be only one of the following:       |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `maxEpsilonPerQuery`                                                                                    | `number` Optional. The maximum epsilon value that a query can consume. If the subscriber specifies epsilon as a parameter in a SELECT query, it must be less than or equal to this value. The epsilon parameter controls the amount of noise that is added to the groups — a higher epsilon means less noise.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
|                                                                                                         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| Union field `_delta_per_query` . `_delta_per_query` can be only one of the following:                   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `deltaPerQuery`                                                                                         | `number` Optional. The delta value that is used per query. Delta represents the probability that any row will fail to be epsilon differentially private. Indicates the risk associated with exposing aggregate rows in the result of a query.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
|                                                                                                         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| Union field `_max_groups_contributed` . `_max_groups_contributed` can be only one of the following:     |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `maxGroupsContributed`                                                                                  | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Optional. The maximum groups contributed value that is used per query. Represents the maximum number of groups to which each protected entity can contribute. Changing this value does not improve or worsen privacy. The best value for accuracy and utility depends on the query and data.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
|                                                                                                         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| Union field `_privacy_unit_column` . `_privacy_unit_column` can be only one of the following:           |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `privacyUnitColumn`                                                                                     | `string` Optional. The privacy unit column associated with this policy. Differential privacy policies can only have one privacy unit column per data source object (table, view).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
|                                                                                                         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| Union field `_epsilon_budget` . `_epsilon_budget` can be only one of the following:                     |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `epsilonBudget`                                                                                         | `number` Optional. The total epsilon budget for all queries against the privacy-protected view. Each subscriber query against this view charges the amount of epsilon they request in their query. If there is sufficient budget, then the subscriber query attempts to complete. It might still fail due to other reasons, in which case the charge is refunded. If there is insufficient budget the query is rejected. There might be multiple charge attempts if a single query references multiple views. In this case there must be sufficient budget for all charges or the query is rejected and charges are refunded in best effort. The budget does not have a refresh policy and can only be updated via ALTER VIEW or circumvented by creating a new view that can be queried with a fresh budget.                                                         |
|                                                                                                         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| Union field `_delta_budget` . `_delta_budget` can be only one of the following:                         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `deltaBudget`                                                                                           | `number` Optional. The total delta budget for all queries against the privacy-protected view. Each subscriber query against this view charges the amount of delta that is pre-defined by the contributor through the privacy policy delta_per_query field. If there is sufficient budget, then the subscriber query attempts to complete. It might still fail due to other reasons, in which case the charge is refunded. If there is insufficient budget the query is rejected. There might be multiple charge attempts if a single query references multiple views. In this case there must be sufficient budget for all charges or the query is rejected and charges are refunded in best effort. The budget does not have a refresh policy and can only be updated via ALTER VIEW or circumvented by creating a new view that can be queried with a fresh budget. |
|                                                                                                         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| Union field `_epsilon_budget_remaining` . `_epsilon_budget_remaining` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `epsilonBudgetRemaining`                                                                                | `number` Output only. The epsilon budget remaining. If budget is exhausted, no more queries are allowed. Note that the budget for queries that are in progress is deducted before the query executes. If the query fails or is cancelled then the budget is refunded. In this case the amount of budget remaining can increase.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
|                                                                                                         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| Union field `_delta_budget_remaining` . `_delta_budget_remaining` can be only one of the following:     |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `deltaBudgetRemaining`                                                                                  | `number` Output only. The delta budget remaining. If budget is exhausted, no more queries are allowed. Note that the budget for queries that are in progress is deducted before the query executes. If the query fails or is cancelled then the budget is refunded. In this case the amount of budget remaining can increase.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
|                                                                                                         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |

### JoinRestrictionPolicy

**JSON representation**

```
{
  "joinAllowedColumns": [
    string
  ],

  // Union field _join_condition can be only one of the following:
  "joinCondition": enum (JoinCondition)
  // End of list of possible types for union field _join_condition.
}
```

| Fields                                                                              |                                                                                                                                                                                                                                                                  |
|-------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `joinAllowedColumns[]`                                                              | `string` Optional. The only columns that joins are allowed on. This field is must be specified for join_conditions JOIN_ANY and JOIN_ALL and it cannot be set for JOIN_BLOCKED.                                                                                  |
| Union field `_join_condition` . `_join_condition` can be only one of the following: |                                                                                                                                                                                                                                                                  |
| `joinCondition`                                                                     | `enum ( `[`JoinCondition`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.JoinCondition)` )` Optional. Specifies if a join is required or not on queries for the view. Default is JOIN_CONDITION_UNSPECIFIED. |
|                                                                                     |                                                                                                                                                                                                                                                                  |

### ForeignViewDefinition

**JSON representation**

```
{
  "query": string,
  "dialect": string
}
```

| Fields    |                                                         |
|-----------|---------------------------------------------------------|
| `query`   | `string` Required. The query that defines the view.     |
| `dialect` | `string` Optional. Represents the dialect of the query. |

### MaterializedViewDefinition

**JSON representation**

```
{
  "query": string,
  "lastRefreshTime": string,
  "enableRefresh": boolean,
  "refreshIntervalMs": string,
  "allowNonIncrementalDefinition": boolean
}
```

| Fields                          |                                                                                                                                                                                                                                                                                                                 |
|---------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `query`                         | `string` Required. A query whose results are persisted.                                                                                                                                                                                                                                                         |
| `lastRefreshTime`               | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Output only. The time when this materialized view was last refreshed, in milliseconds since the epoch.                                                                                                                   |
| `enableRefresh`                 | `boolean` Optional. Enable automatic refresh of the materialized view when the base table is updated. The default value is "true".                                                                                                                                                                              |
| `refreshIntervalMs`             | `string ( `[`UInt64Value`](https://developers.google.com/discovery/v1/type-format)` format)` Optional. The maximum frequency at which this materialized view will be refreshed. The default value is "1800000" (30 minutes).                                                                                    |
| `allowNonIncrementalDefinition` | `boolean` Optional. This option declares the intention to construct a materialized view that isn't refreshed incrementally. Non-incremental materialized views support an expanded range of SQL queries. The `allow_non_incremental_definition` option can't be changed after the materialized view is created. |

### MaterializedViewStatus

**JSON representation**

```
{
  "refreshWatermark": string,
  "lastRefreshStatus": {
    object (ErrorProto)
  }
}
```

| Fields              |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
|---------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `refreshWatermark`  | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. Refresh watermark of materialized view. The base tables' data were collected into the materialized view cache until this time. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` . |
| `lastRefreshStatus` | `object ( `[`ErrorProto`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.ErrorProto)` )` Output only. Error result of the last automatic refresh. If present, indicates that the last automatic refresh was unsuccessful.                                                                                                                                                                                                                                      |

### Timestamp

**JSON representation**

```
{
  "seconds": string,
  "nanos": integer
}
```

| Fields    |                                                                                                                                                                                                                                                                                                                      |
|-----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `seconds` | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Represents seconds of UTC time since Unix epoch 1970-01-01T00:00:00Z. Must be between -62135596800 and 253402300799 inclusive (which corresponds to 0001-01-01T00:00:00Z to 9999-12-31T23:59:59Z).                            |
| `nanos`   | `integer` Non-negative fractions of a second at nanosecond resolution. This field is the nanosecond portion of the duration, not an alternative to seconds. Negative second values with fractions must still have non-negative nanos values that count forward in time. Must be between 0 and 999,999,999 inclusive. |

### ErrorProto

**JSON representation**

```
{
  "reason": string,
  "location": string,
  "debugInfo": string,
  "message": string
}
```

| Fields      |                                                                                             |
|-------------|---------------------------------------------------------------------------------------------|
| `reason`    | `string` A short error code that summarizes the error.                                      |
| `location`  | `string` Specifies where the error occurred, if present.                                    |
| `debugInfo` | `string` Debugging information. This property is internal to Google and should not be used. |
| `message`   | `string` A human-readable description of the error.                                         |

### ExternalDataConfiguration

**JSON representation**

```
{
  "sourceUris": [
    string
  ],
  "fileSetSpecType": enum (FileSetSpecType),
  "schema": {
    object (TableSchema)
  },
  "sourceFormat": string,
  "maxBadRecords": integer,
  "autodetect": boolean,
  "ignoreUnknownValues": boolean,
  "compression": string,
  "csvOptions": {
    object (CsvOptions)
  },
  "jsonOptions": {
    object (JsonOptions)
  },
  "bigtableOptions": {
    object (BigtableOptions)
  },
  "googleSheetsOptions": {
    object (GoogleSheetsOptions)
  },
  "hivePartitioningOptions": {
    object (HivePartitioningOptions)
  },
  "connectionId": string,
  "decimalTargetTypes": [
    enum (DecimalTargetType)
  ],
  "avroOptions": {
    object (AvroOptions)
  },
  "jsonExtension": enum (JsonExtension),
  "parquetOptions": {
    object (ParquetOptions)
  },
  "referenceFileSchemaUri": string,
  "metadataCacheMode": enum (MetadataCacheMode),
  "timestampTargetPrecision": [
    integer
  ],

  // Union field _object_metadata can be only one of the following:
  "objectMetadata": enum (ObjectMetadata)
  // End of list of possible types for union field _object_metadata.

  // Union field _time_zone can be only one of the following:
  "timeZone": string
  // End of list of possible types for union field _time_zone.

  // Union field _date_format can be only one of the following:
  "dateFormat": string
  // End of list of possible types for union field _date_format.

  // Union field _datetime_format can be only one of the following:
  "datetimeFormat": string
  // End of list of possible types for union field _datetime_format.

  // Union field _time_format can be only one of the following:
  "timeFormat": string
  // End of list of possible types for union field _time_format.

  // Union field _timestamp_format can be only one of the following:
  "timestampFormat": string
  // End of list of possible types for union field _timestamp_format.
}
```

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
<td><code>sourceUris[]</code></td>
<td><p><code>string</code></p>
<p>[Required] The fully-qualified URIs that point to your data in Google Cloud. For Google Cloud Storage URIs: Each URI can contain one '*' wildcard character and it must come after the 'bucket' name. Size limits related to load jobs apply to external data sources. For Google Cloud Bigtable URIs: Exactly one URI can be specified and it has be a fully specified and valid HTTPS URL for a Google Cloud Bigtable table. For Google Cloud Datastore backups, exactly one URI can be specified. Also, the '*' wildcard character is not allowed.</p></td>
</tr>
<tr class="even">
<td><code>fileSetSpecType</code></td>
<td><p><code>enum ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.FileSetSpecType"><code>FileSetSpecType</code></a><code> )</code></p>
<p>Optional. Specifies how source URIs are interpreted for constructing the file set to load. By default source URIs are expanded against the underlying storage. Other options include specifying manifest files. Only applicable to object storage systems.</p></td>
</tr>
<tr class="odd">
<td><code>schema</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.TableSchema"><code>TableSchema</code></a><code> )</code></p>
<p>Optional. The schema for the data. Schema is required for CSV and JSON formats if autodetect is not on. Schema is disallowed for Google Cloud Bigtable, Cloud Datastore backups, Avro, ORC and Parquet formats.</p></td>
</tr>
<tr class="even">
<td><code>sourceFormat</code></td>
<td><p><code>string</code></p>
<p>[Required] The data format. For CSV files, specify "CSV". For Google sheets, specify "GOOGLE_SHEETS". For newline-delimited JSON, specify "NEWLINE_DELIMITED_JSON". For Avro files, specify "AVRO". For Google Cloud Datastore backups, specify "DATASTORE_BACKUP". For Apache Iceberg tables, specify "ICEBERG". For ORC files, specify "ORC". For Parquet files, specify "PARQUET". [Beta] For Google Cloud Bigtable, specify "BIGTABLE".</p></td>
</tr>
<tr class="odd">
<td><code>maxBadRecords</code></td>
<td><p><code>integer</code></p>
<p>Optional. The maximum number of bad records that BigQuery can ignore when reading data. If the number of bad records exceeds this value, an invalid error is returned in the job result. The default value is 0, which requires that all records are valid. This setting is ignored for Google Cloud Bigtable, Google Cloud Datastore backups, Avro, ORC and Parquet formats.</p></td>
</tr>
<tr class="even">
<td><code>autodetect</code></td>
<td><p><code>boolean</code></p>
<p>Try to detect schema and format options automatically. Any option specified explicitly will be honored.</p></td>
</tr>
<tr class="odd">
<td><code>ignoreUnknownValues</code></td>
<td><p><code>boolean</code></p>
<p>Optional. Indicates if BigQuery should allow extra values that are not represented in the table schema. If true, the extra values are ignored. If false, records with extra columns are treated as bad records, and if there are too many bad records, an invalid error is returned in the job result. The default value is false. The sourceFormat property determines what BigQuery treats as an extra value: CSV: Trailing columns JSON: Named values that don't match any column names Google Cloud Bigtable: This setting is ignored. Google Cloud Datastore backups: This setting is ignored. Avro: This setting is ignored. ORC: This setting is ignored. Parquet: This setting is ignored.</p></td>
</tr>
<tr class="even">
<td><code>compression</code></td>
<td><p><code>string</code></p>
<p>Optional. The compression type of the data source. Possible values include GZIP and NONE. The default value is NONE. This setting is ignored for Google Cloud Bigtable, Google Cloud Datastore backups, Avro, ORC and Parquet formats. An empty string is an invalid value.</p></td>
</tr>
<tr class="odd">
<td><code>csvOptions</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.CsvOptions"><code>CsvOptions</code></a><code> )</code></p>
<p>Optional. Additional properties to set if sourceFormat is set to CSV.</p></td>
</tr>
<tr class="even">
<td><code>jsonOptions</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.JsonOptions"><code>JsonOptions</code></a><code> )</code></p>
<p>Optional. Additional properties to set if sourceFormat is set to JSON.</p></td>
</tr>
<tr class="odd">
<td><code>bigtableOptions</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.BigtableOptions"><code>BigtableOptions</code></a><code> )</code></p>
<p>Optional. Additional options if sourceFormat is set to BIGTABLE.</p></td>
</tr>
<tr class="even">
<td><code>googleSheetsOptions</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.GoogleSheetsOptions"><code>GoogleSheetsOptions</code></a><code> )</code></p>
<p>Optional. Additional options if sourceFormat is set to GOOGLE_SHEETS.</p></td>
</tr>
<tr class="odd">
<td><code>hivePartitioningOptions</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.HivePartitioningOptions"><code>HivePartitioningOptions</code></a><code> )</code></p>
<p>Optional. When set, configures hive partitioning support. Not all storage formats support hive partitioning -- requesting hive partitioning on an unsupported format will lead to an error, as will providing an invalid specification.</p></td>
</tr>
<tr class="even">
<td><code>connectionId</code></td>
<td><p><code>string</code></p>
<p>Optional. The connection specifying the credentials to be used to read external storage, such as Azure Blob, Cloud Storage, or S3. The connection_id can have the form <code>{project_id}.{location_id};{connection_id}</code> or <code>projects/{project_id}/locations/{location_id}/connections/{connection_id}</code> .</p></td>
</tr>
<tr class="odd">
<td><code>decimalTargetTypes[]</code></td>
<td><p><code>enum ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.DecimalTargetType"><code>DecimalTargetType</code></a><code> )</code></p>
<p>Defines the list of possible SQL data types to which the source decimal values are converted. This list and the precision and the scale parameters of the decimal field determine the target type. In the order of NUMERIC, BIGNUMERIC, and STRING, a type is picked if it is in the specified list and if it supports the precision and the scale. STRING supports all precision and scale values. If none of the listed types supports the precision and the scale, the type supporting the widest range in the specified list is picked, and if a value exceeds the supported range when reading the data, an error will be thrown.</p>
<p>Example: Suppose the value of this field is ["NUMERIC", "BIGNUMERIC"]. If (precision,scale) is:</p>
<ul>
<li>(38,9) -&gt; NUMERIC;</li>
<li>(39,9) -&gt; BIGNUMERIC (NUMERIC cannot hold 30 integer digits);</li>
<li>(38,10) -&gt; BIGNUMERIC (NUMERIC cannot hold 10 fractional digits);</li>
<li>(76,38) -&gt; BIGNUMERIC;</li>
<li>(77,38) -&gt; BIGNUMERIC (error if value exceeds supported range).</li>
</ul>
<p>This field cannot contain duplicate types. The order of the types in this field is ignored. For example, ["BIGNUMERIC", "NUMERIC"] is the same as ["NUMERIC", "BIGNUMERIC"] and NUMERIC always takes precedence over BIGNUMERIC.</p>
<p>Defaults to ["NUMERIC", "STRING"] for ORC and ["NUMERIC"] for the other file formats.</p></td>
</tr>
<tr class="even">
<td><code>avroOptions</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.AvroOptions"><code>AvroOptions</code></a><code> )</code></p>
<p>Optional. Additional properties to set if sourceFormat is set to AVRO.</p></td>
</tr>
<tr class="odd">
<td><code>jsonExtension</code></td>
<td><p><code>enum ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.JsonExtension"><code>JsonExtension</code></a><code> )</code></p>
<p>Optional. Load option to be used together with source_format newline-delimited JSON to indicate that a variant of JSON is being loaded. To load newline-delimited GeoJSON, specify GEOJSON (and source_format must be set to NEWLINE_DELIMITED_JSON).</p></td>
</tr>
<tr class="even">
<td><code>parquetOptions</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.ParquetOptions"><code>ParquetOptions</code></a><code> )</code></p>
<p>Optional. Additional properties to set if sourceFormat is set to PARQUET.</p></td>
</tr>
<tr class="odd">
<td><code>referenceFileSchemaUri</code></td>
<td><p><code>string</code></p>
<p>Optional. When creating an external table, the user can provide a reference file with the table schema. This is enabled for the following formats: AVRO, PARQUET, ORC.</p></td>
</tr>
<tr class="even">
<td><code>metadataCacheMode</code></td>
<td><p><code>enum ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.MetadataCacheMode"><code>MetadataCacheMode</code></a><code> )</code></p>
<p>Optional. Metadata Cache Mode for the table. Set this to enable caching of metadata from external data source.</p></td>
</tr>
<tr class="odd">
<td><code>timestampTargetPrecision[]</code></td>
<td><p><code>integer</code></p>
<p>Precisions (maximum number of total digits in base 10) for seconds of TIMESTAMP types that are allowed to the destination table for autodetection mode.</p>
<p>Available for the formats: CSV, PARQUET, AVRO, and Iceberg External Table.</p>
<p>Possible values include: Not Specified, [], or [6]: timestamp(6) for all auto detected TIMESTAMP columns [6, 12]: timestamp(6) for all auto detected TIMESTAMP columns that have less than 6 digits of subseconds. timestamp(12) for all auto detected TIMESTAMP columns that have more than 6 digits of subseconds. [12]: timestamp(12) for all auto detected TIMESTAMP columns.</p>
<p>The order of the elements in this array is ignored. Inputs that have higher precision than the highest target precision in this array will be truncated.</p></td>
</tr>
<tr class="even">
<td><p>Union field <code>_object_metadata</code> .</p>
<p><code>_object_metadata</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="odd">
<td><code>objectMetadata</code></td>
<td><p><code>enum ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.ObjectMetadata"><code>ObjectMetadata</code></a><code> )</code></p>
<p>Optional. ObjectMetadata is used to create Object Tables. Object Tables contain a listing of objects (with their metadata) found at the source_uris. If ObjectMetadata is set, source_format should be omitted.</p>
<p>Currently SIMPLE is the only supported Object Metadata type.</p></td>
</tr>
<tr class="even">
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p>Union field <code>_time_zone</code> .</p>
<p><code>_time_zone</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="even">
<td><code>timeZone</code></td>
<td><p><code>string</code></p>
<p>Optional. Time zone used when parsing timestamp values that do not have specific time zone information (e.g. 2024-04-20 12:34:56). The expected format is a IANA timezone string (e.g. America/Los_Angeles).</p></td>
</tr>
<tr class="odd">
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p>Union field <code>_date_format</code> .</p>
<p><code>_date_format</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="odd">
<td><code>dateFormat</code></td>
<td><p><code>string</code></p>
<p>Optional. Format used to parse DATE values. Supports C-style and SQL-style values.</p></td>
</tr>
<tr class="even">
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p>Union field <code>_datetime_format</code> .</p>
<p><code>_datetime_format</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="even">
<td><code>datetimeFormat</code></td>
<td><p><code>string</code></p>
<p>Optional. Format used to parse DATETIME values. Supports C-style and SQL-style values.</p></td>
</tr>
<tr class="odd">
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p>Union field <code>_time_format</code> .</p>
<p><code>_time_format</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="odd">
<td><code>timeFormat</code></td>
<td><p><code>string</code></p>
<p>Optional. Format used to parse TIME values. Supports C-style and SQL-style values.</p></td>
</tr>
<tr class="even">
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p>Union field <code>_timestamp_format</code> .</p>
<p><code>_timestamp_format</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="even">
<td><code>timestampFormat</code></td>
<td><p><code>string</code></p>
<p>Optional. Format used to parse TIMESTAMP values. Supports C-style and SQL-style values.</p></td>
</tr>
<tr class="odd">
<td></td>
<td></td>
</tr>
</tbody>
</table>

### Int32Value

**JSON representation**

```
{
  "value": integer
}
```

| Fields  |                            |
|---------|----------------------------|
| `value` | `integer` The int32 value. |

### CsvOptions

**JSON representation**

```
{
  "fieldDelimiter": string,
  "skipLeadingRows": string,
  "quote": string,
  "allowQuotedNewlines": boolean,
  "allowJaggedRows": boolean,
  "encoding": string,
  "preserveAsciiControlCharacters": boolean,
  "nullMarker": string,
  "nullMarkers": [
    string
  ],
  "sourceColumnMatch": string
}
```

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
<td><code>fieldDelimiter</code></td>
<td><p><code>string</code></p>
<p>Optional. The separator character for fields in a CSV file. The separator is interpreted as a single byte. For files encoded in ISO-8859-1, any single character can be used as a separator. For files encoded in UTF-8, characters represented in decimal range 1-127 (U+0001-U+007F) can be used without any modification. UTF-8 characters encoded with multiple bytes (i.e. U+0080 and above) will have only the first byte used for separating fields. The remaining bytes will be treated as a part of the field. BigQuery also supports the escape sequence "\t" (U+0009) to specify a tab separator. The default value is comma (",", U+002C).</p></td>
</tr>
<tr class="even">
<td><code>skipLeadingRows</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>Int64Value</code></a><code> format)</code></p>
<p>Optional. The number of rows at the top of a CSV file that BigQuery will skip when reading the data. The default value is 0. This property is useful if you have header rows in the file that should be skipped. When autodetect is on, the behavior is the following:</p>
<ul>
<li>skipLeadingRows unspecified - Autodetect tries to detect headers in the first row. If they are not detected, the row is read as data. Otherwise data is read starting from the second row.</li>
<li>skipLeadingRows is 0 - Instructs autodetect that there are no headers and data should be read starting from the first row.</li>
<li>skipLeadingRows = N &gt; 0 - Autodetect skips N-1 rows and tries to detect headers in row N. If headers are not detected, row N is just skipped. Otherwise row N is used to extract column names for the detected schema.</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>quote</code></td>
<td><p><code>string</code></p>
<p>Optional. The value that is used to quote data sections in a CSV file. BigQuery converts the string to ISO-8859-1 encoding, and then uses the first byte of the encoded string to split the data in its raw, binary state. The default value is a double-quote ("). If your data does not contain quoted sections, set the property value to an empty string. If your data contains quoted newline characters, you must also set the allowQuotedNewlines property to true. To include the specific quote character within a quoted value, precede it with an additional matching quote character. For example, if you want to escape the default character ' " ', use ' "" '.</p></td>
</tr>
<tr class="even">
<td><code>allowQuotedNewlines</code></td>
<td><p><code>boolean</code></p>
<p>Optional. Indicates if BigQuery should allow quoted data sections that contain newline characters in a CSV file. The default value is false.</p></td>
</tr>
<tr class="odd">
<td><code>allowJaggedRows</code></td>
<td><p><code>boolean</code></p>
<p>Optional. Indicates if BigQuery should accept rows that are missing trailing optional columns. If true, BigQuery treats missing trailing columns as null values. If false, records with missing trailing columns are treated as bad records, and if there are too many bad records, an invalid error is returned in the job result. The default value is false.</p></td>
</tr>
<tr class="even">
<td><code>encoding</code></td>
<td><p><code>string</code></p>
<p>Optional. The character encoding of the data. The supported values are UTF-8, ISO-8859-1, UTF-16BE, UTF-16LE, UTF-32BE, and UTF-32LE. The default value is UTF-8. BigQuery decodes the data after the raw, binary data has been split using the values of the quote and fieldDelimiter properties.</p></td>
</tr>
<tr class="odd">
<td><code>preserveAsciiControlCharacters</code></td>
<td><p><code>boolean</code></p>
<p>Optional. Indicates if the embedded ASCII control characters (the first 32 characters in the ASCII-table, from '\x00' to '\x1F') are preserved.</p></td>
</tr>
<tr class="even">
<td><code>nullMarker</code></td>
<td><p><code>string</code></p>
<p>Optional. Specifies a string that represents a null value in a CSV file. For example, if you specify "\N", BigQuery interprets "\N" as a null value when querying a CSV file. The default value is the empty string. If you set this property to a custom value, BigQuery throws an error if an empty string is present for all data types except for STRING and BYTE. For STRING and BYTE columns, BigQuery interprets the empty string as an empty value.</p></td>
</tr>
<tr class="odd">
<td><code>nullMarkers[]</code></td>
<td><p><code>string</code></p>
<p>Optional. A list of strings represented as SQL NULL value in a CSV file.</p>
<p>null_marker and null_markers can't be set at the same time. If null_marker is set, null_markers has to be not set. If null_markers is set, null_marker has to be not set. If both null_marker and null_markers are set at the same time, a user error would be thrown. Any strings listed in null_markers, including empty string would be interpreted as SQL NULL. This applies to all column types.</p></td>
</tr>
<tr class="even">
<td><code>sourceColumnMatch</code></td>
<td><p><code>string</code></p>
<p>Optional. Controls the strategy used to match loaded columns to the schema. If not set, a sensible default is chosen based on how the schema is provided. If autodetect is used, then columns are matched by name. Otherwise, columns are matched by position. This is done to keep the behavior backward-compatible. Acceptable values are: POSITION - matches by position. This assumes that the columns are ordered the same way as the schema. NAME - matches by name. This reads the header row as column names and reorders columns to match the field names in the schema.</p></td>
</tr>
</tbody>
</table>

### JsonOptions

**JSON representation**

```
{
  "encoding": string
}
```

| Fields     |                                                                                                                                                                |
|------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `encoding` | `string` Optional. The character encoding of the data. The supported values are UTF-8, UTF-16BE, UTF-16LE, UTF-32BE, and UTF-32LE. The default value is UTF-8. |

### BigtableOptions

**JSON representation**

```
{
  "columnFamilies": [
    {
      object (BigtableColumnFamily)
    }
  ],
  "ignoreUnspecifiedColumnFamilies": boolean,
  "readRowkeyAsString": boolean,
  "outputColumnFamiliesAsJson": boolean
}
```

| Fields                            |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
|-----------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `columnFamilies[]`                | `object ( `[`BigtableColumnFamily`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.BigtableColumnFamily)` )` Optional. List of column families to expose in the table schema along with their types. This list restricts the column families that can be referenced in queries and specifies their value types. You can use this list to do type conversions - see the 'type' field for more details. If you leave this list empty, all column families are present in the table schema and their values are read as BYTES. During a query only the column families referenced in that query are read from Bigtable. |
| `ignoreUnspecifiedColumnFamilies` | `boolean` Optional. If field is true, then the column families that are not specified in columnFamilies list are not exposed in the table schema. Otherwise, they are read with BYTES type values. The default value is false.                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| `readRowkeyAsString`              | `boolean` Optional. If field is true, then the rowkey column families will be read and converted to string. Otherwise they are read with BYTES type values and users need to manually cast them with CAST if necessary. The default value is false.                                                                                                                                                                                                                                                                                                                                                                                                                     |
| `outputColumnFamiliesAsJson`      | `boolean` Optional. If field is true, then each column family will be read as a single JSON column. Otherwise they are read as a repeated cell structure containing timestamp/value tuples. The default value is false.                                                                                                                                                                                                                                                                                                                                                                                                                                                 |

### BigtableColumnFamily

**JSON representation**

```
{
  "familyId": string,
  "type": string,
  "encoding": string,
  "columns": [
    {
      object (BigtableColumn)
    }
  ],
  "onlyReadLatest": boolean,
  "protoConfig": {
    object (BigtableProtoConfig)
  }
}
```

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
<td><code>familyId</code></td>
<td><p><code>string</code></p>
<p>Identifier of the column family.</p></td>
</tr>
<tr class="even">
<td><code>type</code></td>
<td><p><code>string</code></p>
<p>Optional. The type to convert the value in cells of this column family. The values are expected to be encoded using HBase Bytes.toBytes function when using the BINARY encoding value. Following BigQuery types are allowed (case-sensitive):</p>
<ul>
<li>BYTES</li>
<li>STRING</li>
<li>INTEGER</li>
<li>FLOAT</li>
<li>BOOLEAN</li>
<li>JSON</li>
</ul>
<p>Default type is BYTES. This can be overridden for a specific column by listing that column in 'columns' and specifying a type for it.</p></td>
</tr>
<tr class="odd">
<td><code>encoding</code></td>
<td><p><code>string</code></p>
<p>Optional. The encoding of the values when the type is not STRING. Acceptable encoding values are: TEXT - indicates values are alphanumeric text strings. BINARY - indicates values are encoded using HBase Bytes.toBytes family of functions. PROTO_BINARY - indicates values are encoded using serialized proto messages. This can only be used in combination with JSON type. This can be overridden for a specific column by listing that column in 'columns' and specifying an encoding for it.</p></td>
</tr>
<tr class="even">
<td><code>columns[]</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.BigtableColumn"><code>BigtableColumn</code></a><code> )</code></p>
<p>Optional. Lists of columns that should be exposed as individual fields as opposed to a list of (column name, value) pairs. All columns whose qualifier matches a qualifier in this list can be accessed as <code>&lt;family field name&gt;.&lt;column field name&gt;</code> . Other columns can be accessed as a list through the <code>&lt;family field name&gt;.Column</code> field.</p></td>
</tr>
<tr class="odd">
<td><code>onlyReadLatest</code></td>
<td><p><code>boolean</code></p>
<p>Optional. If this is set only the latest version of value are exposed for all columns in this column family. This can be overridden for a specific column by listing that column in 'columns' and specifying a different setting for that column.</p></td>
</tr>
<tr class="even">
<td><code>protoConfig</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.BigtableProtoConfig"><code>BigtableProtoConfig</code></a><code> )</code></p>
<p>Optional. Protobuf-specific configurations, only takes effect when the encoding is PROTO_BINARY.</p></td>
</tr>
</tbody>
</table>

### BigtableColumn

**JSON representation**

```
{
  "qualifierEncoded": string,
  "qualifierString": string,
  "fieldName": string,
  "type": string,
  "encoding": string,
  "onlyReadLatest": boolean,
  "protoConfig": {
    object (BigtableProtoConfig)
  }
}
```

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
<td><code>qualifierEncoded</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>BytesValue</code></a><code> format)</code></p>
<p>[Required] Qualifier of the column. Columns in the parent column family that has this exact qualifier are exposed as <code>&lt;family field name&gt;.&lt;column field name&gt;</code> field. If the qualifier is valid UTF-8 string, it can be specified in the qualifier_string field. Otherwise, a base-64 encoded value must be set to qualifier_encoded. The column field name is the same as the column qualifier. However, if the qualifier is not a valid BigQuery field identifier i.e. does not match [a-zA-Z][a-zA-Z0-9_]*, a valid identifier must be provided as field_name.</p></td>
</tr>
<tr class="even">
<td><code>qualifierString</code></td>
<td><p><code>string</code></p>
<p>Qualifier string.</p></td>
</tr>
<tr class="odd">
<td><code>fieldName</code></td>
<td><p><code>string</code></p>
<p>Optional. If the qualifier is not a valid BigQuery field identifier i.e. does not match [a-zA-Z][a-zA-Z0-9_]*, a valid identifier must be provided as the column field name and is used as field name in queries.</p></td>
</tr>
<tr class="even">
<td><code>type</code></td>
<td><p><code>string</code></p>
<p>Optional. The type to convert the value in cells of this column. The values are expected to be encoded using HBase Bytes.toBytes function when using the BINARY encoding value. Following BigQuery types are allowed (case-sensitive):</p>
<ul>
<li>BYTES</li>
<li>STRING</li>
<li>INTEGER</li>
<li>FLOAT</li>
<li>BOOLEAN</li>
<li>JSON</li>
</ul>
<p>Default type is BYTES. 'type' can also be set at the column family level. However, the setting at this level takes precedence if 'type' is set at both levels.</p></td>
</tr>
<tr class="odd">
<td><code>encoding</code></td>
<td><p><code>string</code></p>
<p>Optional. The encoding of the values when the type is not STRING. Acceptable encoding values are: TEXT - indicates values are alphanumeric text strings. BINARY - indicates values are encoded using HBase Bytes.toBytes family of functions. PROTO_BINARY - indicates values are encoded using serialized proto messages. This can only be used in combination with JSON type. 'encoding' can also be set at the column family level. However, the setting at this level takes precedence if 'encoding' is set at both levels.</p></td>
</tr>
<tr class="even">
<td><code>onlyReadLatest</code></td>
<td><p><code>boolean</code></p>
<p>Optional. If this is set, only the latest version of value in this column are exposed. 'onlyReadLatest' can also be set at the column family level. However, the setting at this level takes precedence if 'onlyReadLatest' is set at both levels.</p></td>
</tr>
<tr class="odd">
<td><code>protoConfig</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.BigtableProtoConfig"><code>BigtableProtoConfig</code></a><code> )</code></p>
<p>Optional. Protobuf-specific configurations, only takes effect when the encoding is PROTO_BINARY.</p></td>
</tr>
</tbody>
</table>

### BytesValue

**JSON representation**

```
{
  "value": string
}
```

| Fields  |                                                                                                                                  |
|---------|----------------------------------------------------------------------------------------------------------------------------------|
| `value` | `string ( `[`bytes`](https://developers.google.com/discovery/v1/type-format)` format)` The bytes value. A base64-encoded string. |

### BigtableProtoConfig

**JSON representation**

```
{
  "schemaBundleId": string,
  "protoMessageName": string
}
```

| Fields             |                                                                                                                                                                                                                                                                                                                                                                                      |
|--------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `schemaBundleId`   | `string` Optional. The ID of the Bigtable SchemaBundle resource associated with this protobuf. The ID should be referred to within the parent table, e.g., `foo` rather than `projects/{project}/instances/{instance}/tables/{table}/schemaBundles/foo` . See [more details on Bigtable SchemaBundles](https://docs.cloud.google.com/bigtable/docs/create-manage-protobuf-schemas) . |
| `protoMessageName` | `string` Optional. The fully qualified proto message name of the protobuf. In the format of "foo.bar.Message".                                                                                                                                                                                                                                                                       |

### GoogleSheetsOptions

**JSON representation**

```
{
  "skipLeadingRows": string,
  "range": string
}
```

| Fields            |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
|-------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `skipLeadingRows` | `string ( `[`Int64Value`](https://developers.google.com/discovery/v1/type-format)` format)` Optional. The number of rows at the top of a sheet that BigQuery will skip when reading the data. The default value is 0. This property is useful if you have header rows that should be skipped. When autodetect is on, the behavior is the following: \* skipLeadingRows unspecified - Autodetect tries to detect headers in the first row. If they are not detected, the row is read as data. Otherwise data is read starting from the second row. \* skipLeadingRows is 0 - Instructs autodetect that there are no headers and data should be read starting from the first row. \* skipLeadingRows = N \> 0 - Autodetect skips N-1 rows and tries to detect headers in row N. If headers are not detected, row N is just skipped. Otherwise row N is used to extract column names for the detected schema. |
| `range`           | `string` Optional. Range of a sheet to query from. Only used when non-empty. Typical format: sheet_name!top_left_cell_id:bottom_right_cell_id For example: sheet1!A1:B20                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |

### HivePartitioningOptions

**JSON representation**

```
{
  "mode": string,
  "sourceUriPrefix": string,
  "requirePartitionFilter": boolean,
  "fields": [
    string
  ]
}
```

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
<td><code>mode</code></td>
<td><p><code>string</code></p>
<p>Optional. When set, what mode of hive partitioning to use when reading data. The following modes are supported:</p>
<ul>
<li><p>AUTO: automatically infer partition key name(s) and type(s).</p></li>
<li><p>STRINGS: automatically infer partition key name(s). All types are strings.</p></li>
<li><p>CUSTOM: partition key schema is encoded in the source URI prefix.</p></li>
</ul>
<p>Not all storage formats support hive partitioning. Requesting hive partitioning on an unsupported format will lead to an error. Currently supported formats are: JSON, CSV, ORC, Avro and Parquet.</p></td>
</tr>
<tr class="even">
<td><code>sourceUriPrefix</code></td>
<td><p><code>string</code></p>
<p>Optional. When hive partition detection is requested, a common prefix for all source uris must be required. The prefix must end immediately before the partition key encoding begins. For example, consider files following this data layout:</p>
<p>gs://bucket/path_to_table/dt=2019-06-01/country=USA/id=7/file.avro</p>
<p>gs://bucket/path_to_table/dt=2019-05-31/country=CA/id=3/file.avro</p>
<p>When hive partitioning is requested with either AUTO or STRINGS detection, the common prefix can be either of gs://bucket/path_to_table or gs://bucket/path_to_table/.</p>
<p>CUSTOM detection requires encoding the partitioning schema immediately after the common prefix. For CUSTOM, any of</p>
<ul>
<li><p>gs://bucket/path_to_table/{dt:DATE}/{country:STRING}/{id:INTEGER}</p></li>
<li><p>gs://bucket/path_to_table/{dt:STRING}/{country:STRING}/{id:INTEGER}</p></li>
<li><p>gs://bucket/path_to_table/{dt:DATE}/{country:STRING}/{id:STRING}</p></li>
</ul>
<p>would all be valid source URI prefixes.</p></td>
</tr>
<tr class="odd">
<td><code>requirePartitionFilter</code></td>
<td><p><code>boolean</code></p>
<p>Optional. If set to true, queries over this table require a partition filter that can be used for partition elimination to be specified.</p>
<p>Note that this field should only be true when creating a permanent external table or querying a temporary external table.</p>
<p>Hive-partitioned loads with require_partition_filter explicitly set to true will fail.</p></td>
</tr>
<tr class="even">
<td><code>fields[]</code></td>
<td><p><code>string</code></p>
<p>Output only. For permanent external tables, this field is populated with the hive partition keys in the order they were inferred. The types of the partition keys can be deduced by checking the table schema (which will include the partition keys). Not every API will populate this field in the output. For example, Tables.Get will populate it, but Tables.List will not contain this field.</p></td>
</tr>
</tbody>
</table>

### AvroOptions

**JSON representation**

```
{
  "useAvroLogicalTypes": boolean
}
```

| Fields                |                                                                                                                                                                                                                            |
|-----------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `useAvroLogicalTypes` | `boolean` Optional. If sourceFormat is set to "AVRO", indicates whether to interpret logical types as the corresponding BigQuery data type (for example, TIMESTAMP), instead of using the raw type (for example, INTEGER). |

### ParquetOptions

**JSON representation**

```
{
  "enumAsString": boolean,
  "enableListInference": boolean,
  "mapTargetType": enum (MapTargetType)
}
```

| Fields                |                                                                                                                                                                                                                |
|-----------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `enumAsString`        | `boolean` Optional. Indicates whether to infer Parquet ENUM logical type as STRING instead of BYTES by default.                                                                                                |
| `enableListInference` | `boolean` Optional. Indicates whether to use schema inference specifically for Parquet LIST logical type.                                                                                                      |
| `mapTargetType`       | `enum ( `[`MapTargetType`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.MapTargetType)` )` Optional. Indicates how to represent a Parquet map if present. |

### BigLakeConfiguration

**JSON representation**

```
{
  "connectionId": string,
  "storageUri": string,
  "fileFormat": enum (FileFormat),
  "tableFormat": enum (TableFormat)
}
```

| Fields         |                                                                                                                                                                                                                                                                                             |
|----------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `connectionId` | `string` Optional. The connection specifying the credentials to be used to read and write to external storage, such as Cloud Storage. The connection_id can have the form `{project}.{location}.{connection_id}` or \`projects/{project}/locations/{location}/connections/{connection_id}". |
| `storageUri`   | `string` Optional. The fully qualified location prefix of the external folder where table data is stored. The '\*' wildcard character is not allowed. The URI should be in the format `gs://bucket/path_to_table/`                                                                          |
| `fileFormat`   | `enum ( `[`FileFormat`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.FileFormat)` )` Optional. The file format the table data is stored in.                                                                                            |
| `tableFormat`  | `enum ( `[`TableFormat`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.TableFormat)` )` Optional. The table format the metadata only snapshots are stored in.                                                                           |

### Streamingbuffer

**JSON representation**

```
{
  "estimatedBytes": string,
  "estimatedRows": string,
  "oldestEntryTime": string
}
```

| Fields            |                                                                                                                                                                                                                                                 |
|-------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `estimatedBytes`  | `string` Output only. A lower-bound estimate of the number of bytes currently in the streaming buffer.                                                                                                                                          |
| `estimatedRows`   | `string` Output only. A lower-bound estimate of the number of rows currently in the streaming buffer.                                                                                                                                           |
| `oldestEntryTime` | `string ( `[`uint64`](https://developers.google.com/discovery/v1/type-format)` format)` Output only. Contains the timestamp of the oldest entry in the streaming buffer, in milliseconds since the epoch, if the streaming buffer is available. |

### EncryptionConfiguration

**JSON representation**

```
{
  "kmsKeyName": string
}
```

| Fields       |                                                                                                                                                                                                                      |
|--------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `kmsKeyName` | `string` Optional. Describes the Cloud KMS encryption key that will be used to protect destination BigQuery table. The BigQuery Service Account associated with your project requires access to this encryption key. |

### SnapshotDefinition

**JSON representation**

```
{
  "baseTableReference": {
    object (TableReference)
  },
  "snapshotTime": string
}
```

| Fields               |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
|----------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `baseTableReference` | `object ( `[`TableReference`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_dataset_info#Output.Schema.TableReference)` )` Required. Reference describing the ID of the table that was snapshot.                                                                                                                                                                                                                                                                      |
| `snapshotTime`       | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Required. The time at which the base table was snapshot. This value is reported in the JSON response using RFC3339 format. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` . |

### CloneDefinition

**JSON representation**

```
{
  "baseTableReference": {
    object (TableReference)
  },
  "cloneTime": string
}
```

| Fields               |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
|----------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `baseTableReference` | `object ( `[`TableReference`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_dataset_info#Output.Schema.TableReference)` )` Required. Reference describing the ID of the table that was cloned.                                                                                                                                                                                                                                                                      |
| `cloneTime`          | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Required. The time at which the base table was cloned. This value is reported in the JSON response using RFC3339 format. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` . |

### RestrictionConfig

**JSON representation**

```
{
  "type": enum (RestrictionType)
}
```

| Fields |                                                                                                                                                                                                                     |
|--------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `type` | `enum ( `[`RestrictionType`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_dataset_info#Output.Schema.RestrictionType)` )` Output only. Specifies the type of dataset/table restriction. |

### TableConstraints

**JSON representation**

```
{
  "primaryKey": {
    object (PrimaryKey)
  },
  "foreignKeys": [
    {
      object (ForeignKey)
    }
  ]
}
```

| Fields          |                                                                                                                                                                                                                                                                                               |
|-----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `primaryKey`    | `object ( `[`PrimaryKey`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.PrimaryKey)` )` Optional. Represents a primary key constraint on a table's columns. Present only if the table has a primary key. The primary key is not enforced. |
| `foreignKeys[]` | `object ( `[`ForeignKey`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.ForeignKey)` )` Optional. Present only if the table has a foreign key. The foreign key is not enforced.                                                           |

### PrimaryKey

**JSON representation**

```
{
  "columns": [
    string
  ]
}
```

| Fields      |                                                                                 |
|-------------|---------------------------------------------------------------------------------|
| `columns[]` | `string` Required. The columns that are composed of the primary key constraint. |

### ForeignKey

**JSON representation**

```
{
  "name": string,
  "referencedTable": {
    object (TableReference)
  },
  "columnReferences": [
    {
      object (ColumnReference)
    }
  ]
}
```

| Fields               |                                                                                                                                                                                                                                             |
|----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`               | `string` Optional. Set only if the foreign key constraint is named.                                                                                                                                                                         |
| `referencedTable`    | `object ( `[`TableReference`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_dataset_info#Output.Schema.TableReference)` )` Required. The table that holds the primary key and is referenced by this foreign key. |
| `columnReferences[]` | `object ( `[`ColumnReference`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.ColumnReference)` )` Required. The columns that compose the foreign key.                                   |

### ColumnReference

**JSON representation**

```
{
  "referencingColumn": string,
  "referencedColumn": string
}
```

| Fields              |                                                                                                 |
|---------------------|-------------------------------------------------------------------------------------------------|
| `referencingColumn` | `string` Required. The column that composes the foreign key.                                    |
| `referencedColumn`  | `string` Required. The column in the primary key that are referenced by the referencing_column. |

### ResourceTagsEntry

**JSON representation**

```
{
  "key": string,
  "value": string
}
```

| Fields  |          |
|---------|----------|
| `key`   | `string` |
| `value` | `string` |

### TableReplicationInfo

**JSON representation**

```
{
  "sourceTable": {
    object (TableReference)
  },
  "replicationIntervalMs": string,
  "replicatedSourceLastRefreshTime": string,
  "replicationStatus": enum (ReplicationStatus),
  "replicationError": {
    object (ErrorProto)
  }
}
```

| Fields                            |                                                                                                                                                                                                                                                          |
|-----------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `sourceTable`                     | `object ( `[`TableReference`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_dataset_info#Output.Schema.TableReference)` )` Required. Source table reference that is replicated.                                               |
| `replicationIntervalMs`           | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Optional. Specifies the interval at which the source table is polled for updates. It's Optional. If not specified, default replication interval would be applied. |
| `replicatedSourceLastRefreshTime` | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Optional. Output only. If source is a materialized view, this field signifies the last refresh time of the source.                                                |
| `replicationStatus`               | `enum ( `[`ReplicationStatus`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.ReplicationStatus)` )` Optional. Output only. Replication status of configured replication.                             |
| `replicationError`                | `object ( `[`ErrorProto`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.ErrorProto)` )` Optional. Output only. Replication error that will permanently stopped table replication.                    |

### ExternalCatalogTableOptions

**JSON representation**

```
{
  "parameters": {
    string: string,
    ...
  },
  "storageDescriptor": {
    object (StorageDescriptor)
  },
  "connectionId": string
}
```

| Fields              |                                                                                                                                                                                                                                                                                                                                                                                                      |
|---------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `parameters`        | `map (key: string, value: string)` Optional. A map of the key-value pairs defining the parameters and properties of the open source table. Corresponds with Hive metastore table parameters. Maximum size of 4MiB. An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .                                                             |
| `storageDescriptor` | `object ( `[`StorageDescriptor`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.StorageDescriptor)` )` Optional. A storage descriptor containing information about the physical storage of this table.                                                                                                                                            |
| `connectionId`      | `string` Optional. A connection ID that specifies the credentials to be used to read external storage, such as Azure Blob, Cloud Storage, or Amazon S3. This connection is needed to read the open source table from BigQuery. The connection_id format must be either `<project_id>.<location_id>.<connection_id>` or `projects/<project_id>/locations/<location_id>/connections/<connection_id>` . |

### ParametersEntry

**JSON representation**

```
{
  "key": string,
  "value": string
}
```

| Fields  |          |
|---------|----------|
| `key`   | `string` |
| `value` | `string` |

### StorageDescriptor

**JSON representation**

```
{
  "locationUri": string,
  "inputFormat": string,
  "outputFormat": string,
  "serdeInfo": {
    object (SerDeInfo)
  }
}
```

| Fields         |                                                                                                                                                                                                     |
|----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `locationUri`  | `string` Optional. The physical location of the table (e.g. `gs://spark-dataproc-data/pangea-data/case_sensitive/` or `gs://spark-dataproc-data/pangea-data/*` ). The maximum length is 2056 bytes. |
| `inputFormat`  | `string` Optional. Specifies the fully qualified class name of the InputFormat (e.g. "org.apache.hadoop.hive.ql.io.orc.OrcInputFormat"). The maximum length is 128 characters.                      |
| `outputFormat` | `string` Optional. Specifies the fully qualified class name of the OutputFormat (e.g. "org.apache.hadoop.hive.ql.io.orc.OrcOutputFormat"). The maximum length is 128 characters.                    |
| `serdeInfo`    | `object ( `[`SerDeInfo`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_table_info#Output.Schema.SerDeInfo)` )` Optional. Serializer and deserializer information.        |

### SerDeInfo

**JSON representation**

```
{
  "name": string,
  "serializationLibrary": string,
  "parameters": {
    string: string,
    ...
  }
}
```

| Fields                 |                                                                                                                                                                                                                                                                                  |
|------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`                 | `string` Optional. Name of the SerDe. The maximum length is 256 characters.                                                                                                                                                                                                      |
| `serializationLibrary` | `string` Required. Specifies a fully-qualified class name of the serialization library that is responsible for the translation of data between table representation and the underlying low-level input and output format structures. The maximum length is 256 characters.       |
| `parameters`           | `map (key: string, value: string)` Optional. Key-value pairs that define the initialization parameters for the serialization library. Maximum size 10 Kib. An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` . |

### ParametersEntry

**JSON representation**

```
{
  "key": string,
  "value": string
}
```

| Fields  |          |
|---------|----------|
| `key`   | `string` |
| `value` | `string` |

### RoundingMode

Rounding mode options that can be used when storing NUMERIC or BIGNUMERIC values.

| Enums                       |                                                                                                                                                                                                                                  |
|-----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `ROUNDING_MODE_UNSPECIFIED` | Unspecified will default to using ROUND_HALF_AWAY_FROM_ZERO.                                                                                                                                                                     |
| `ROUND_HALF_AWAY_FROM_ZERO` | ROUND_HALF_AWAY_FROM_ZERO rounds half values away from zero when applying precision and scale upon writing of NUMERIC and BIGNUMERIC values. For Scale: 0 1.1, 1.2, 1.3, 1.4 =\> 1 1.5, 1.6, 1.7, 1.8, 1.9 =\> 2                 |
| `ROUND_HALF_EVEN`           | ROUND_HALF_EVEN rounds half values to the nearest even value when applying precision and scale upon writing of NUMERIC and BIGNUMERIC values. For Scale: 0 1.1, 1.2, 1.3, 1.4 =\> 1 1.5 =\> 2 1.6, 1.7, 1.8, 1.9 =\> 2 2.5 =\> 2 |

### GeneratedMode

Dictates when system generated values are used to populate the field.

| Enums                        |                                                                                                  |
|------------------------------|--------------------------------------------------------------------------------------------------|
| `GENERATED_MODE_UNSPECIFIED` | Unspecified GeneratedMode will default to GENERATED_ALWAYS.                                      |
| `GENERATED_ALWAYS`           | Field can only have system generated values. Users cannot manually insert values into the field. |
| `GENERATED_BY_DEFAULT`       | Use system generated values only if the user does not explicitly provide a value.                |

### TypeSystem

External systems, such as query engines or table formats, that have their own data types.

| Enums                     |                             |
|---------------------------|-----------------------------|
| `TYPE_SYSTEM_UNSPECIFIED` | TypeSystem not specified.   |
| `HIVE`                    | Represents Hive data types. |

### JoinCondition

Enum for Join Restrictions policy.

| Enums                        |                                                                                       |
|------------------------------|---------------------------------------------------------------------------------------|
| `JOIN_CONDITION_UNSPECIFIED` | A join is neither required nor restricted on any column. Default value.               |
| `JOIN_ANY`                   | A join is required on at least one of the specified columns.                          |
| `JOIN_ALL`                   | A join is required on all specified columns.                                          |
| `JOIN_NOT_REQUIRED`          | A join is not required, but if present it is only permitted on 'join_allowed_columns' |
| `JOIN_BLOCKED`               | Joins are blocked for all queries.                                                    |

### FileSetSpecType

This enum defines how to interpret source URIs for load jobs and external tables.

| Enums                                            |                                                                                                                                            |
|--------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------|
| `FILE_SET_SPEC_TYPE_FILE_SYSTEM_MATCH`           | This option expands source URIs by listing files from the object store. It is the default behavior if FileSetSpecType is not set.          |
| `FILE_SET_SPEC_TYPE_NEW_LINE_DELIMITED_MANIFEST` | This option indicates that the provided URIs are newline-delimited manifest files, with one URI per line. Wildcard URIs are not supported. |

### DecimalTargetType

The data types that could be used as a target type when converting decimal values.

| Enums                             |                                                       |
|-----------------------------------|-------------------------------------------------------|
| `DECIMAL_TARGET_TYPE_UNSPECIFIED` | Invalid type.                                         |
| `NUMERIC`                         | Decimal values could be converted to NUMERIC type.    |
| `BIGNUMERIC`                      | Decimal values could be converted to BIGNUMERIC type. |
| `STRING`                          | Decimal values could be converted to STRING type.     |

### JsonExtension

Used to indicate that a JSON variant, rather than normal JSON, is being used as the source_format. This should only be used in combination with the JSON source format.

| Enums                        |                                                                                                                                                     |
|------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------|
| `JSON_EXTENSION_UNSPECIFIED` | The default if provided value is not one included in the enum, or the value is not specified. The source format is parsed without any modification. |
| `GEOJSON`                    | Use GeoJSON variant of JSON. See <https://tools.ietf.org/html/rfc7946> .                                                                            |

### MapTargetType

Indicates the map target type. Only applies to parquet maps.

| Enums                         |                                                                                                                          |
|-------------------------------|--------------------------------------------------------------------------------------------------------------------------|
| `MAP_TARGET_TYPE_UNSPECIFIED` | In this mode, the map will have the following schema: struct map_field_name { repeated struct key_value { key value } }. |
| `ARRAY_OF_STRUCT`             | In this mode, the map will have the following schema: repeated struct map_field_name { key value }.                      |

### ObjectMetadata

Supported Object Metadata Types.

| Enums                         |                               |
|-------------------------------|-------------------------------|
| `OBJECT_METADATA_UNSPECIFIED` | Unspecified by default.       |
| `DIRECTORY`                   | A synonym for `SIMPLE` .      |
| `SIMPLE`                      | Directory listing of objects. |

### MetadataCacheMode

MetadataCacheMode identifies if the table should use metadata caching for files from external source (eg Google Cloud Storage).

| Enums                             |                                                                                                                                                                                                      |
|-----------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `METADATA_CACHE_MODE_UNSPECIFIED` | Unspecified metadata cache mode.                                                                                                                                                                     |
| `AUTOMATIC`                       | Set this mode to trigger automatic background refresh of metadata cache from the external source. Queries will use the latest available cache version within the table's maxStaleness interval.      |
| `MANUAL`                          | Set this mode to enable triggering manual refresh of the metadata cache from external source. Queries will use the latest manually triggered cache version within the table's maxStaleness interval. |

### FileFormat

Supported file formats for BigQuery tables for Apache Iceberg.

| Enums                     |                        |
|---------------------------|------------------------|
| `FILE_FORMAT_UNSPECIFIED` | Default Value.         |
| `PARQUET`                 | Apache Parquet format. |

### TableFormat

Supported table formats for BigQuery tables for Apache Iceberg.

| Enums                      |                        |
|----------------------------|------------------------|
| `TABLE_FORMAT_UNSPECIFIED` | Default Value.         |
| `ICEBERG`                  | Apache Iceberg format. |

### ManagedTableType

The classification of managed table types that can be created.

| Enums                            |                                                                      |
|----------------------------------|----------------------------------------------------------------------|
| `MANAGED_TABLE_TYPE_UNSPECIFIED` | No managed table type specified.                                     |
| `NATIVE`                         | The managed table is a native BigQuery table.                        |
| `BIGLAKE`                        | The managed table is a BigLake table for Apache Iceberg in BigQuery. |

### RestrictionType

RestrictionType specifies the type of dataset/table restriction.

| Enums                          |                                                                                                                                          |
|--------------------------------|------------------------------------------------------------------------------------------------------------------------------------------|
| `RESTRICTION_TYPE_UNSPECIFIED` | Should never be used.                                                                                                                    |
| `RESTRICTED_DATA_EGRESS`       | Restrict data egress. See [Data egress](https://cloud.google.com/bigquery/docs/analytics-hub-introduction#data_egress) for more details. |

### ReplicationStatus

Replication status of the table created using `AS REPLICA` like: `CREATE MATERIALIZED VIEW mv1 AS REPLICA OF src_mv`

| Enums                            |                                                 |
|----------------------------------|-------------------------------------------------|
| `REPLICATION_STATUS_UNSPECIFIED` | Default value.                                  |
| `ACTIVE`                         | Replication is Active with no errors.           |
| `SOURCE_DELETED`                 | Source object is deleted.                       |
| `PERMISSION_DENIED`              | Source revoked replication permissions.         |
| `UNSUPPORTED_CONFIGURATION`      | Source configuration doesn't allow replication. |

### Tool Annotations

[Tool annotations](https://modelcontextprotocol.io/specification/latest/schema#toolannotations) are sent to MCP clients to describe the basic risk of a given tool. Most clients treat these hints as untrusted, but they can be used to decide when a confirmation prompt might be sent to a user.

Along with the title string, the following boolean hints are defined as follows:

- `readOnlyHint` : If true, the tool doesn't modify its environment. Default: false.
- `destructiveHint` : If true, then the tool can perform destructive actions. If false, then the tool can only perform additive actions. Default: true.
- `idempotentHint` : If true, then calling the tool repeatedly with the same arguments will have no additional effect on its environment. Default: false.
- `openWorldHint` : If true, then the tool can interact with an 'open world' of external entities. If false, then the tool can only interact with internal entities. For example, a web search tool would be open world, while a memory tool would not be open world.

Destructive Hint: ❌ \| Idempotent Hint: ✅ \| Read Only Hint: ✅ \| Open World Hint: ❌
