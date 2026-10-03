---
name: documents/docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_dataset_info
uri: https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_dataset_info
title: 'MCP Tools Reference: bigquery.googleapis.com'
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

## Tool: `get_dataset_info`

Get metadata information about a BigQuery dataset or BigLake namespace.

The following code sample shows how to use `curl` to call the `get_dataset_info` MCP tool.

**Curl Request**

```
curl --location 'https://bigquery.googleapis.com/mcp' \
--header 'content-type: application/json' \
--header 'accept: application/json, text/event-stream' \
--data '{
  "method": "tools/call",
  "params": {
    "name": "get_dataset_info",
    "arguments": {
      // Provide these details according to the MCP tool specification.
    }
  },
  "jsonrpc": "2.0",
  "id": 1
}'
```

## Input Schema

Request for a dataset.

### GetDatasetRequest

**JSON representation**

```
{
  "projectId": string,
  "datasetId": string
}
```

| Fields      |                                                       |
|-------------|-------------------------------------------------------|
| `projectId` | `string` Required. Project ID of the dataset request. |
| `datasetId` | `string` Required. Dataset ID of the dataset request. |

## Output Schema

Represents a BigQuery dataset.

### Dataset

**JSON representation**

```
{
  "kind": string,
  "etag": string,
  "id": string,
  "selfLink": string,
  "datasetReference": {
    object (DatasetReference)
  },
  "friendlyName": string,
  "description": string,
  "defaultTableExpirationMs": string,
  "defaultPartitionExpirationMs": string,
  "labels": {
    string: string,
    ...
  },
  "access": [
    {
      object (Access)
    }
  ],
  "creationTime": string,
  "lastModifiedTime": string,
  "location": string,
  "defaultEncryptionConfiguration": {
    object (EncryptionConfiguration)
  },
  "satisfiesPzs": boolean,
  "satisfiesPzi": boolean,
  "type": string,
  "linkedDatasetSource": {
    object (LinkedDatasetSource)
  },
  "linkedDatasetMetadata": {
    object (LinkedDatasetMetadata)
  },
  "externalDatasetReference": {
    object (ExternalDatasetReference)
  },
  "externalCatalogDatasetOptions": {
    object (ExternalCatalogDatasetOptions)
  },
  "isCaseInsensitive": boolean,
  "defaultCollation": string,
  "defaultRoundingMode": enum (RoundingMode),
  "maxTimeTravelHours": string,
  "tags": [
    {
      object (GcpTag)
    }
  ],
  "storageBillingModel": enum (StorageBillingModel),
  "restrictions": {
    object (RestrictionConfig)
  },
  "resourceTags": {
    string: string,
    ...
  },

  // Union field _catalog_source can be only one of the following:
  "catalogSource": string
  // End of list of possible types for union field _catalog_source.
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
<p>Output only. The resource type.</p></td>
</tr>
<tr class="even">
<td><code>etag</code></td>
<td><p><code>string</code></p>
<p>Output only. A hash of the resource.</p></td>
</tr>
<tr class="odd">
<td><code>id</code></td>
<td><p><code>string</code></p>
<p>Output only. The fully-qualified unique name of the dataset in the format projectId:datasetId. The dataset name without the project name is given in the datasetId field. When creating a new dataset, leave this field blank, and instead specify the datasetId field.</p></td>
</tr>
<tr class="even">
<td><code>selfLink</code></td>
<td><p><code>string</code></p>
<p>Output only. A URL that can be used to access the resource again. You can use this URL in Get or Update requests to the resource.</p></td>
</tr>
<tr class="odd">
<td><code>datasetReference</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_dataset_info#Output.Schema.DatasetReference"><code>DatasetReference</code></a><code> )</code></p>
<p>Required. A reference that identifies the dataset.</p></td>
</tr>
<tr class="even">
<td><code>friendlyName</code></td>
<td><p><code>string</code></p>
<p>Optional. A descriptive name for the dataset.</p></td>
</tr>
<tr class="odd">
<td><code>description</code></td>
<td><p><code>string</code></p>
<p>Optional. A user-friendly description of the dataset.</p></td>
</tr>
<tr class="even">
<td><code>defaultTableExpirationMs</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>Int64Value</code></a><code> format)</code></p>
<p>Optional. The default lifetime of all tables in the dataset, in milliseconds. The minimum lifetime value is 3600000 milliseconds (one hour). To clear an existing default expiration with a PATCH request, set to 0. Once this property is set, all newly-created tables in the dataset will have an expirationTime property set to the creation time plus the value in this property, and changing the value will only affect new tables, not existing ones. When the expirationTime for a given table is reached, that table will be deleted automatically. If a table's expirationTime is modified or removed before the table expires, or if you provide an explicit expirationTime when creating a table, that value takes precedence over the default expiration time indicated by this property.</p></td>
</tr>
<tr class="odd">
<td><code>defaultPartitionExpirationMs</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>Int64Value</code></a><code> format)</code></p>
<p>This default partition expiration, expressed in milliseconds.</p>
<p>When new time-partitioned tables are created in a dataset where this property is set, the table will inherit this value, propagated as the <code>TimePartitioning.expirationMs</code> property on the new table. If you set <code>TimePartitioning.expirationMs</code> explicitly when creating a table, the <code>defaultPartitionExpirationMs</code> of the containing dataset is ignored.</p>
<p>When creating a partitioned table, if <code>defaultPartitionExpirationMs</code> is set, the <code>defaultTableExpirationMs</code> value is ignored and the table will not be inherit a table expiration deadline.</p></td>
</tr>
<tr class="even">
<td><code>labels</code></td>
<td><p><code>map (key: string, value: string)</code></p>
<p>The labels associated with this dataset. You can use these to organize and group your datasets. You can set this property when inserting or updating a dataset. See <a href="https://cloud.google.com/bigquery/docs/creating-managing-labels#creating_and_updating_dataset_labels">Creating and Updating Dataset Labels</a> for more information.</p>
<p>An object containing a list of <code>"key": value</code> pairs. Example: <code>{ "name": "wrench", "mass": "1.3kg", "count": "3" }</code> .</p></td>
</tr>
<tr class="odd">
<td><code>access[]</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_dataset_info#Output.Schema.Access"><code>Access</code></a><code> )</code></p>
<p>Optional. An array of objects that define dataset access for one or more entities. You can set this property when inserting or updating a dataset in order to control who is allowed to access the data. If unspecified at dataset creation time, BigQuery adds default dataset access for the following entities: access.specialGroup: projectReaders; access.role: READER; access.specialGroup: projectWriters; access.role: WRITER; access.specialGroup: projectOwners; access.role: OWNER; access.userByEmail: [dataset creator email]; access.role: OWNER; If you patch a dataset, then this field is overwritten by the patched dataset's access field. To add entities, you must supply the entire existing access array in addition to any new entities that you want to add.</p></td>
</tr>
<tr class="even">
<td><code>creationTime</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>int64</code></a><code> format)</code></p>
<p>Output only. The time when this dataset was created, in milliseconds since the epoch.</p></td>
</tr>
<tr class="odd">
<td><code>lastModifiedTime</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>int64</code></a><code> format)</code></p>
<p>Output only. The date when this dataset was last modified, in milliseconds since the epoch.</p></td>
</tr>
<tr class="even">
<td><code>location</code></td>
<td><p><code>string</code></p>
<p>The geographic location where the dataset should reside. See <a href="https://cloud.google.com/bigquery/docs/locations">https://cloud.google.com/bigquery/docs/locations</a> for supported locations.</p></td>
</tr>
<tr class="odd">
<td><code>defaultEncryptionConfiguration</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_dataset_info#Output.Schema.EncryptionConfiguration"><code>EncryptionConfiguration</code></a><code> )</code></p>
<p>The default encryption key for all tables in the dataset. After this property is set, the encryption key of all newly-created tables in the dataset is set to this value unless the table creation request or query explicitly overrides the key.</p></td>
</tr>
<tr class="even">
<td><code>satisfiesPzs</code></td>
<td><p><code>boolean</code></p>
<p>Output only. Reserved for future use.</p></td>
</tr>
<tr class="odd">
<td><code>satisfiesPzi</code></td>
<td><p><code>boolean</code></p>
<p>Output only. Reserved for future use.</p></td>
</tr>
<tr class="even">
<td><code>type</code></td>
<td><p><code>string</code></p>
<p>Output only. Same as <code>type</code> in <code>ListFormatDataset</code> . The type of the dataset, one of:</p>
<ul>
<li>DEFAULT - only accessible by owner and authorized accounts,</li>
<li>PUBLIC - accessible by everyone,</li>
<li>LINKED - linked dataset,</li>
<li>EXTERNAL - dataset with definition in external metadata catalog,</li>
<li>BIGLAKE_ICEBERG - a Biglake dataset accessible through the Iceberg API,</li>
<li>BIGLAKE_HIVE - a Biglake dataset accessible through the Hive API.</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>linkedDatasetSource</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_dataset_info#Output.Schema.LinkedDatasetSource"><code>LinkedDatasetSource</code></a><code> )</code></p>
<p>Optional. The source dataset reference when the dataset is of type LINKED. For all other dataset types it is not set. This field cannot be updated once it is set. Any attempt to update this field using Update and Patch API Operations will be ignored.</p></td>
</tr>
<tr class="even">
<td><code>linkedDatasetMetadata</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_dataset_info#Output.Schema.LinkedDatasetMetadata"><code>LinkedDatasetMetadata</code></a><code> )</code></p>
<p>Output only. Metadata about the LinkedDataset. Filled out when the dataset type is LINKED.</p></td>
</tr>
<tr class="odd">
<td><code>externalDatasetReference</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_dataset_info#Output.Schema.ExternalDatasetReference"><code>ExternalDatasetReference</code></a><code> )</code></p>
<p>Optional. Reference to a read-only external dataset defined in data catalogs outside of BigQuery. Filled out when the dataset type is EXTERNAL.</p></td>
</tr>
<tr class="even">
<td><code>externalCatalogDatasetOptions</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_dataset_info#Output.Schema.ExternalCatalogDatasetOptions"><code>ExternalCatalogDatasetOptions</code></a><code> )</code></p>
<p>Optional. Options defining open source compatible datasets living in the BigQuery catalog. Contains metadata of open source database, schema or namespace represented by the current dataset.</p></td>
</tr>
<tr class="odd">
<td><code>isCaseInsensitive</code></td>
<td><p><code>boolean</code></p>
<p>Optional. TRUE if the dataset and its table names are case-insensitive, otherwise FALSE. By default, this is FALSE, which means the dataset and its table names are case-sensitive. This field does not affect routine references.</p></td>
</tr>
<tr class="even">
<td><code>defaultCollation</code></td>
<td><p><code>string</code></p>
<p>Optional. Defines the default collation specification of future tables created in the dataset. If a table is created in this dataset without table-level default collation, then the table inherits the dataset default collation, which is applied to the string fields that do not have explicit collation specified. A change to this field affects only tables created afterwards, and does not alter the existing tables. The following values are supported:</p>
<ul>
<li>'und:ci': undetermined locale, case insensitive.</li>
<li>'': empty string. Default to case-sensitive behavior.</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>defaultRoundingMode</code></td>
<td><p><code>enum ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_dataset_info#Output.Schema.RoundingMode"><code>RoundingMode</code></a><code> )</code></p>
<p>Optional. Defines the default rounding mode specification of new tables created within this dataset. During table creation, if this field is specified, the table within this dataset will inherit the default rounding mode of the dataset. Setting the default rounding mode on a table overrides this option. Existing tables in the dataset are unaffected. If columns are defined during that table creation, they will immediately inherit the table's default rounding mode, unless otherwise specified.</p></td>
</tr>
<tr class="even">
<td><code>maxTimeTravelHours</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>Int64Value</code></a><code> format)</code></p>
<p>Optional. Defines the time travel window in hours. The value can be from 48 to 168 hours (2 to 7 days). The default value is 168 hours if this is not set.</p></td>
</tr>
<tr class="odd">
<td><code>tags[] </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_dataset_info#Output.Schema.GcpTag"><code>GcpTag</code></a><code> )</code></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>Output only. Tags for the dataset. To provide tags as inputs, use the <code>resourceTags</code> field.</p></td>
</tr>
<tr class="even">
<td><code>storageBillingModel</code></td>
<td><p><code>enum ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_dataset_info#Output.Schema.StorageBillingModel"><code>StorageBillingModel</code></a><code> )</code></p>
<p>Optional. Updates storage_billing_model for the dataset.</p></td>
</tr>
<tr class="odd">
<td><code>restrictions</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_dataset_info#Output.Schema.RestrictionConfig"><code>RestrictionConfig</code></a><code> )</code></p>
<p>Optional. Output only. Restriction config for all tables and dataset. If set, restrict certain accesses on the dataset and all its tables based on the config. See <a href="https://cloud.google.com/bigquery/docs/analytics-hub-introduction#data_egress">Data egress</a> for more details.</p></td>
</tr>
<tr class="even">
<td><code>resourceTags</code></td>
<td><p><code>map (key: string, value: string)</code></p>
<p>Optional. The <a href="https://cloud.google.com/bigquery/docs/tags">tags</a> attached to this dataset. Tag keys are globally unique. Tag key is expected to be in the namespaced format, for example "123456789012/environment" where 123456789012 is the ID of the parent organization or project resource for this tag key. Tag value is expected to be the short name, for example "Production". See <a href="https://cloud.google.com/iam/docs/tags-access-control#definitions">Tag definitions</a> for more details.</p>
<p>An object containing a list of <code>"key": value</code> pairs. Example: <code>{ "name": "wrench", "mass": "1.3kg", "count": "3" }</code> .</p></td>
</tr>
<tr class="odd">
<td><p>Union field <code>_catalog_source</code> .</p>
<p><code>_catalog_source</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="even">
<td><code>catalogSource</code></td>
<td><p><code>string</code></p>
<p>Output only. The origin of the dataset, one of:</p>
<ul>
<li>(Unset) - Native BigQuery Dataset</li>
<li>BIGLAKE - Dataset is backed by a namespace stored natively in Biglake</li>
</ul></td>
</tr>
<tr class="odd">
<td></td>
<td></td>
</tr>
</tbody>
</table>

### DatasetReference

**JSON representation**

```
{
  "datasetId": string,
  "projectId": string
}
```

| Fields      |                                                                                                                                                                                                     |
|-------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `datasetId` | `string` Required. A unique ID for this dataset, without the project name. The ID must contain only letters (a-z, A-Z), numbers (0-9), or underscores (\_). The maximum length is 1,024 characters. |
| `projectId` | `string` Optional. The ID of the project containing this dataset.                                                                                                                                   |

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

### Access

**JSON representation**

```
{
  "role": string,
  "userByEmail": string,
  "groupByEmail": string,
  "domain": string,
  "specialGroup": string,
  "iamMember": string,
  "view": {
    object (TableReference)
  },
  "routine": {
    object (RoutineReference)
  },
  "dataset": {
    object (DatasetAccessEntry)
  },
  "condition": {
    object (Expr)
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
<td><code>role</code></td>
<td><p><code>string</code></p>
<p>An IAM role ID that should be granted to the user, group, or domain specified in this access entry. The following legacy mappings will be applied:</p>
<ul>
<li><code>OWNER</code> : <code>roles/bigquery.dataOwner</code></li>
<li><code>WRITER</code> : <code>roles/bigquery.dataEditor</code></li>
<li><code>READER</code> : <code>roles/bigquery.dataViewer</code></li>
</ul>
<p>This field will accept any of the above formats, but will return only the legacy format. For example, if you set this field to "roles/bigquery.dataOwner", it will be returned back as "OWNER".</p></td>
</tr>
<tr class="even">
<td><code>userByEmail</code></td>
<td><p><code>string</code></p>
<p>[Pick one] An email address of a user to grant access to. For example: <a href="mailto:fred@example.com">fred@example.com</a> . Maps to IAM policy member "user:EMAIL" or "serviceAccount:EMAIL".</p></td>
</tr>
<tr class="odd">
<td><code>groupByEmail</code></td>
<td><p><code>string</code></p>
<p>[Pick one] An email address of a Google Group to grant access to. Maps to IAM policy member "group:GROUP".</p></td>
</tr>
<tr class="even">
<td><code>domain</code></td>
<td><p><code>string</code></p>
<p>[Pick one] A domain to grant access to. Any users signed in with the domain specified will be granted the specified access. Example: "example.com". Maps to IAM policy member "domain:DOMAIN".</p></td>
</tr>
<tr class="odd">
<td><code>specialGroup</code></td>
<td><p><code>string</code></p>
<p>[Pick one] A special group to grant access to. Possible values include:</p>
<ul>
<li>projectOwners: Owners of the enclosing project.</li>
<li>projectReaders: Readers of the enclosing project.</li>
<li>projectWriters: Writers of the enclosing project.</li>
<li>allAuthenticatedUsers: All authenticated BigQuery users.</li>
</ul>
<p>Maps to similarly-named IAM members.</p></td>
</tr>
<tr class="even">
<td><code>iamMember</code></td>
<td><p><code>string</code></p>
<p>[Pick one] Some other type of member that appears in the IAM Policy but isn't a user, group, domain, or special group.</p></td>
</tr>
<tr class="odd">
<td><code>view</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_dataset_info#Output.Schema.TableReference"><code>TableReference</code></a><code> )</code></p>
<p>[Pick one] A view from a different dataset to grant access to. Queries executed against that view will have read access to views/tables/routines in this dataset. The role field is not required when this field is set. If that view is updated by any user, access to the view needs to be granted again via an update operation.</p></td>
</tr>
<tr class="even">
<td><code>routine</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_dataset_info#Output.Schema.RoutineReference"><code>RoutineReference</code></a><code> )</code></p>
<p>[Pick one] A routine from a different dataset to grant access to. Queries executed against that routine will have read access to views/tables/routines in this dataset. Only UDF is supported for now. The role field is not required when this field is set. If that routine is updated by any user, access to the routine needs to be granted again via an update operation.</p></td>
</tr>
<tr class="odd">
<td><code>dataset</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_dataset_info#Output.Schema.DatasetAccessEntry"><code>DatasetAccessEntry</code></a><code> )</code></p>
<p>[Pick one] A grant authorizing all resources of a particular type in a particular dataset access to this dataset. Only views are supported for now. The role field is not required when this field is set. If that dataset is deleted and re-created, its access needs to be granted again via an update operation.</p></td>
</tr>
<tr class="even">
<td><code>condition</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_dataset_info#Output.Schema.Expr"><code>Expr</code></a><code> )</code></p>
<p>Optional. condition for the binding. If CEL expression in this field is true, this access binding will be considered</p></td>
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

### RoutineReference

**JSON representation**

```
{
  "projectId": string,
  "datasetId": string,
  "routineId": string
}
```

| Fields      |                                                                                                                                                                  |
|-------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `projectId` | `string` Required. The ID of the project containing this routine.                                                                                                |
| `datasetId` | `string` Required. The ID of the dataset containing this routine.                                                                                                |
| `routineId` | `string` Required. The ID of the routine. The ID must contain only letters (a-z, A-Z), numbers (0-9), or underscores (\_). The maximum length is 256 characters. |

### DatasetAccessEntry

**JSON representation**

```
{
  "dataset": {
    object (DatasetReference)
  },
  "targetTypes": [
    enum (TargetType)
  ]
}
```

| Fields          |                                                                                                                                                                                                                                                                                                |
|-----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `dataset`       | `object ( `[`DatasetReference`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_dataset_info#Output.Schema.DatasetReference)` )` The dataset this entry applies to                                                                                                    |
| `targetTypes[]` | `enum ( `[`TargetType`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_dataset_info#Output.Schema.TargetType)` )` Which resources in the dataset this entry applies to. Currently, only views are supported, but additional target types may be added in the future. |

### Expr

**JSON representation**

```
{
  "expression": string,
  "title": string,
  "description": string,
  "location": string
}
```

| Fields        |                                                                                                                                                            |
|---------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `expression`  | `string` Textual representation of an expression in Common Expression Language syntax.                                                                     |
| `title`       | `string` Optional. Title for the expression, i.e. a short string describing its purpose. This can be used e.g. in UIs which allow to enter the expression. |
| `description` | `string` Optional. Description of the expression. This is a longer text which describes the expression, e.g. when hovered over it in a UI.                 |
| `location`    | `string` Optional. String indicating the location of the expression for error reporting, e.g. a file name and a position in the file.                      |

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

### LinkedDatasetSource

**JSON representation**

```
{
  "sourceDataset": {
    object (DatasetReference)
  }
}
```

| Fields          |                                                                                                                                                                                                                                      |
|-----------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `sourceDataset` | `object ( `[`DatasetReference`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_dataset_info#Output.Schema.DatasetReference)` )` The source dataset reference contains project numbers and not project ids. |

### LinkedDatasetMetadata

**JSON representation**

```
{
  "linkState": enum (LinkState)
}
```

| Fields      |                                                                                                                                                                                                                                |
|-------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `linkState` | `enum ( `[`LinkState`](https://docs.cloud.google.com/bigquery/docs/reference/mcp/tools_list/get_dataset_info#Output.Schema.LinkState)` )` Output only. Specifies whether Linked Dataset is currently in a linked state or not. |

### ExternalDatasetReference

**JSON representation**

```
{
  "externalSource": string,
  "connection": string
}
```

| Fields           |                                                                                                                                                                    |
|------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `externalSource` | `string` Required. External source that backs this dataset.                                                                                                        |
| `connection`     | `string` Required. The connection id that is used to access the external_source. Format: projects/{project_id}/locations/{location_id}/connections/{connection_id} |

### ExternalCatalogDatasetOptions

**JSON representation**

```
{
  "parameters": {
    string: string,
    ...
  },
  "defaultStorageLocationUri": string
}
```

| Fields                      |                                                                                                                                                                                                                                                                                     |
|-----------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `parameters`                | `map (key: string, value: string)` Optional. A map of key value pairs defining the parameters and properties of the open source schema. Maximum size of 2MiB. An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` . |
| `defaultStorageLocationUri` | `string` Optional. The storage location URI for all tables in the dataset. Equivalent to hive metastore's database locationUri. Maximum length of 1024 characters.                                                                                                                  |

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

### GcpTag

**JSON representation**

```
{
  "tagKey": string,
  "tagValue": string
}
```

| Fields     |                                                                                                                 |
|------------|-----------------------------------------------------------------------------------------------------------------|
| `tagKey`   | `string` Required. The namespaced friendly name of the tag key, e.g. "12345/environment" where 12345 is org id. |
| `tagValue` | `string` Required. The friendly short name of the tag value, e.g. "production".                                 |

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

### TargetType

Indicates the type of resources in a dataset that the entry applies to.

| Enums                     |                                                    |
|---------------------------|----------------------------------------------------|
| `TARGET_TYPE_UNSPECIFIED` | Do not use. You must set a target type explicitly. |
| `VIEWS`                   | This entry applies to views in the dataset.        |
| `ROUTINES`                | This entry applies to routines in the dataset.     |

### LinkState

Specifies whether Linked Dataset is currently in a linked state or not.

| Enums                    |                                                                                                                                   |
|--------------------------|-----------------------------------------------------------------------------------------------------------------------------------|
| `LINK_STATE_UNSPECIFIED` | The default value. Default to the LINKED state.                                                                                   |
| `LINKED`                 | Normal Linked Dataset state. Data is queryable via the Linked Dataset.                                                            |
| `UNLINKED`               | Data publisher or owner has unlinked this Linked Dataset. It means you can no longer query or see the data in the Linked Dataset. |

### RoundingMode

Rounding mode options that can be used when storing NUMERIC or BIGNUMERIC values.

| Enums                       |                                                                                                                                                                                                                                  |
|-----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `ROUNDING_MODE_UNSPECIFIED` | Unspecified will default to using ROUND_HALF_AWAY_FROM_ZERO.                                                                                                                                                                     |
| `ROUND_HALF_AWAY_FROM_ZERO` | ROUND_HALF_AWAY_FROM_ZERO rounds half values away from zero when applying precision and scale upon writing of NUMERIC and BIGNUMERIC values. For Scale: 0 1.1, 1.2, 1.3, 1.4 =\> 1 1.5, 1.6, 1.7, 1.8, 1.9 =\> 2                 |
| `ROUND_HALF_EVEN`           | ROUND_HALF_EVEN rounds half values to the nearest even value when applying precision and scale upon writing of NUMERIC and BIGNUMERIC values. For Scale: 0 1.1, 1.2, 1.3, 1.4 =\> 1 1.5 =\> 2 1.6, 1.7, 1.8, 1.9 =\> 2 2.5 =\> 2 |

### StorageBillingModel

Indicates the billing model that will be applied to the dataset.

| Enums                               |                             |
|-------------------------------------|-----------------------------|
| `STORAGE_BILLING_MODEL_UNSPECIFIED` | Value not set.              |
| `LOGICAL`                           | Billing for logical bytes.  |
| `PHYSICAL`                          | Billing for physical bytes. |

### RestrictionType

RestrictionType specifies the type of dataset/table restriction.

| Enums                          |                                                                                                                                          |
|--------------------------------|------------------------------------------------------------------------------------------------------------------------------------------|
| `RESTRICTION_TYPE_UNSPECIFIED` | Should never be used.                                                                                                                    |
| `RESTRICTED_DATA_EGRESS`       | Restrict data egress. See [Data egress](https://cloud.google.com/bigquery/docs/analytics-hub-introduction#data_egress) for more details. |

### Tool Annotations

[Tool annotations](https://modelcontextprotocol.io/specification/latest/schema#toolannotations) are sent to MCP clients to describe the basic risk of a given tool. Most clients treat these hints as untrusted, but they can be used to decide when a confirmation prompt might be sent to a user.

Along with the title string, the following boolean hints are defined as follows:

- `readOnlyHint` : If true, the tool doesn't modify its environment. Default: false.
- `destructiveHint` : If true, then the tool can perform destructive actions. If false, then the tool can only perform additive actions. Default: true.
- `idempotentHint` : If true, then calling the tool repeatedly with the same arguments will have no additional effect on its environment. Default: false.
- `openWorldHint` : If true, then the tool can interact with an 'open world' of external entities. If false, then the tool can only interact with internal entities. For example, a web search tool would be open world, while a memory tool would not be open world.

Destructive Hint: ❌ \| Idempotent Hint: ✅ \| Read Only Hint: ✅ \| Open World Hint: ❌
