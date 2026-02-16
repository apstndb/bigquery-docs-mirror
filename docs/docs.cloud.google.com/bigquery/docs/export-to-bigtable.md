# Export data to Bigtable (reverse ETL)

This document describes how you can set up reverse ETL (RETL) from BigQuery to Bigtable. You can do this by using the [`  EXPORT DATA  ` statement](/bigquery/docs/reference/standard-sql/export-statements) to export data from a BigQuery table to a [Bigtable](/bigtable/docs/overview) table.

You can use a RETL workflow to Bigtable to combine BigQuery's analytics capabilities with Bigtable's low latency and high throughput. This workflow lets you serve data to application users without exhausting quotas and limits on BigQuery.

## Characteristics of Bigtable tables

[Bigtable tables](/bigtable/docs/overview#storage-model) are different from BigQuery tables in several ways:

  - Both Bigtable and BigQuery tables are made of rows, but a Bigtable row is made of row key and column families that have an arbitrary number of columns belonging to the same column family.
  - Column families for a given table are created at table creation time but can also be added or removed later. When a column family is created, columns that belong to it don't need to be specified.
  - Bigtable columns don't need to be defined ahead of time and can be used to store data in their name (also known as a *qualifier* ) within [data size limits within tables](/bigtable/quotas#limits-data-size) .
  - Bigtable columns can have any binary value within [data size limits within tables](/bigtable/quotas#limits-data-size) .
  - Bigtable columns always have a temporal dimension (also known as *version* ). Any number of values might be stored in any row for the same column as long as the timestamp is not identical.
  - A Bigtable timestamp is measured in microseconds since [Unix epoch time](https://en.wikipedia.org/wiki/Unix_time) —for example, 0 represents 1970-01-01T00:00:00 UTC. Timestamps must be a non-negative number of microseconds with millisecond granularity (only multiples of 1000us are accepted). The default Bigtable timestamp is 0.
  - Data in Bigtable is [read by row key, multiple row keys, range of row keys, or by using a filter](/bigtable/docs/reads) . At least one row key or row keys range is required in all types of read requests except for a full table scan.

For information about preparing BigQuery results for export to Bigtable, see [Prepare query results for export](#prepare_results) .

## Before you begin

You must create a [Bigtable instance](/bigtable/docs/creating-instance) and a [Bigtable table](/bigtable/docs/managing-tables#create-table) to receive the exported data.

Grant [Identity and Access Management (IAM) roles](#required_roles) that give users the necessary permissions to perform each task in this document.

### Required roles

To get the permissions that you need to export BigQuery data to Bigtable, ask your administrator to grant you the following IAM roles on your project:

  - Export data from a BigQuery table: [BigQuery Data Viewer](/iam/docs/roles-permissions/bigquery#bigquery.dataViewer) ( `  roles/bigquery.dataViewer  ` )
  - Run an extract job: [BigQuery User](/iam/docs/roles-permissions/bigquery#bigquery.user) ( `  roles/bigquery.user  ` )
  - Write data to a Bigtable table: [Bigtable User](/iam/docs/roles-permissions/bigtable#bigtable.user) ( `  roles/bigtable.user  ` )
  - Auto-create new column families for a Bigtable table: [Bigtable Administrator](/iam/docs/roles-permissions/bigtable#bigtable.admin) ( `  roles/bigtable.admin  ` )

For more information about granting roles, see [Manage access to projects, folders, and organizations](/iam/docs/granting-changing-revoking-access) .

You might also be able to get the required permissions through [custom roles](/iam/docs/creating-custom-roles) or other [predefined roles](/iam/docs/roles-overview#predefined) .

## Limitations

  - Encoding is limited to `  BINARY  ` and `  TEXT  ` only.
  - The destination [Bigtable app profile](/bigtable/docs/app-profiles) must be configured with [single-cluster routing](/bigtable/docs/routing#single-cluster) and a [low request priority level](/bigtable/docs/request-priorities) .
  - The Bigtable app profile must be configured to route data to a Bigtable cluster colocated with the BigQuery dataset. For more information, see [location considerations](#data-locations) .
  - Exports to Bigtable are only supported for [BigQuery Enterprise or Enterprise Plus editions](/bigquery/docs/editions-intro) . BigQuery Standard edition and [on-demand compute](https://cloud.google.com/bigquery/pricing#on_demand_pricing) are not supported.
  - Exports to Bigtable are only supported for reservations with a [`  QUERY  ` assignment](/bigquery/docs/reservations-assignments) .

## Location considerations

  - If your BigQuery dataset is in a multi-region, your [Bigtable app profile](/bigtable/docs/app-profiles) must be configured to route data to a Bigtable cluster within that multi-region. For example, if your BigQuery dataset is in the `  US  ` multi-region, the Bigtable cluster can be located in the `  us-west1  ` (Oregon) region, which is within the United States.
  - If your BigQuery dataset is in a single region, your [Bigtable app profile](/bigtable/docs/app-profiles) must be configured to route data to a Bigtable cluster in the same region. For example, if your BigQuery dataset is in the `  asia-northeast1  ` (Tokyo) region, your Bigtable cluster must also be in the `  asia-northeast1  ` (Tokyo) region.

For more information, see [Bigtable locations](/bigtable/docs/locations) .

## Supported BigQuery types

The following types of data are supported when they're written to Bigtable:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>BigQuery type</th>
<th>Bigtable value written</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       BYTES      </code></td>
<td>Exported as is.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Converted to <code dir="ltr" translate="no">       BYTES      </code> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td>If <code dir="ltr" translate="no">       bigtable_options.column_families.encoding      </code> is set to <code dir="ltr" translate="no">       BINARY      </code> , then the value is written in an 8 byte, big-endian format (most significant byte first). If <code dir="ltr" translate="no">       bigtable_options.column_families.encoding      </code> is set to <code dir="ltr" translate="no">       TEXT      </code> , then the value is written as a human-readable string representing a number.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       FLOAT      </code></td>
<td>Writes value in the IEEE 754 8-byte output format.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       BOOLEAN      </code></td>
<td>If <code dir="ltr" translate="no">       bigtable_options.column_families.encoding      </code> is set to <code dir="ltr" translate="no">       BINARY      </code> , then the value is written as a 1 byte value ( <code dir="ltr" translate="no">       false      </code> = 0x00 or <code dir="ltr" translate="no">       true      </code> = 0x01). If <code dir="ltr" translate="no">       bigtable_options.column_families.encoding      </code> is set to <code dir="ltr" translate="no">       TEXT      </code> , then the value is written as a text ( <code dir="ltr" translate="no">       "true"      </code> or <code dir="ltr" translate="no">       "false"      </code> ).</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       JSON      </code></td>
<td>An exported column of <code dir="ltr" translate="no">        JSON       </code> type is interpreted as a group of columns belonging to a specific Bigtable column family. Members of the JSON object are interpreted as columns and their values are to be written to Bigtable. The name of the column to be written can be adjusted using the <a href="#bigtable_options"><code dir="ltr" translate="no">         bigtable_options        </code></a> configuration.
<br />

For example:
<pre class="text" dir="ltr" data-is-upgraded="" data-syntax="JSON" translate="no"><code>    JSON &#39;{&quot;FIELD1&quot;: &quot;VALUE1&quot;, &quot;FIELD2&quot;: &quot;VALUE2&quot;}&#39; as MY_COLUMN_FAMILY
    </code></pre>
Where values VALUE1 and VALUE2 are written to Bigtable as columns FIELD1 and FIELD2 to the column family MY_COLUMN_FAMILY .
<strong>Note:</strong> A JSON document nested in another <code dir="ltr" translate="no">        JSON       </code> or <code dir="ltr" translate="no">        STRUCT       </code> type is written to Bigtable as a string. Exporting a <code dir="ltr" translate="no">        STRUCT       </code> value nested in another struct is subject to limitations explained in the <a href="#bigtable_options">Configure exports with <code dir="ltr" translate="no">         bigtable_options        </code></a> section.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       STRUCT      </code></td>
<td>An exported column of <code dir="ltr" translate="no">        STRUCT       </code> type is interpreted as a group of columns belonging to a specific Bigtable column family. Members of the struct are interpreted as columns and their values to be written to Bigtable. The name of the column to be written can be adjusted using the <a href="#bigtable_options"><code dir="ltr" translate="no">         bigtable_options        </code></a> configuration.
<br />

For example:
<pre class="text" dir="ltr" data-is-upgraded="" data-syntax="JSON" translate="no"><code>    STRUCT&lt;FIELD1  STRING, FIELD2 INTEGER&gt; as MY_COLUMN_FAMILY
    </code></pre>
Where values FIELD1 and FIELD2 are written to Bigtable as columns FIELD1 and FIELD2 to the column family MY_COLUMN_FAMILY .</td>
</tr>
</tbody>
</table>

These supported data types are similar to reading from [external Bigtable tables](/bigquery/docs/reference/rest/v2/tables#bigtablecolumnfamily) for BigQuery.

## `     NULL    ` values in Bigtable

`  NULL  ` values in Bigtable have the following constraints:

  - Bigtable has no analog for `  NULL  ` values. Exporting a `  NULL  ` value for a given column family and column in Bigtable deletes the present values from a Bigtable row.

  - If a Bigtable value with a given row key, column family, column qualifier, and timestamp doesn't exist prior to the export, the exported `  NULL  ` values have no effect on the Bigtable row.

  - When exporting a `  NULL  ` value of the `  STRUCT  ` or `  JSON  ` type, all column values belonging to the corresponding column family of the affected row are deleted. You should cast the `  NULL  ` value to the `  STRUCT  ` or `  JSON  ` type in order for the SQL engine to attach a correct type to it. The following query deletes all data from column family `  column_family1  ` with a set of given rowkeys:
    
    ``` text
    EXPORT DATA OPTIONS (...) AS
    SELECT
      rowkey,
    CAST(NULL as STRUCT<INT64>) AS column_family1 FROM T
    ```

  - Rows with `  NULL  ` row keys are skipped during the export. The number of skipped rows is returned in export statistics to the caller.

## Configure exports with `     bigtable_options    `

You can use the `  bigtable_options  ` configuration during an export to bridge the differences between BigQuery and Bigtable storage models. The configuration is expressed in the form of a JSON string, as seen in the following example:

``` text
EXPORT DATA OPTIONS(
   uri="https://bigtable.googleapis.com/projects/PROJECT_ID/instances/INSTANCE_ID/appProfiles/APP_PROFILE_ID/tables/TABLE",
   bigtable_options = """{
     "columnFamilies": [{
       "familyId": "COLUMN_FAMILY_NAME",
       "encoding": "ENCODING_VALUE",
       "columns": [
         {
           "qualifierString": "BIGTABLE_COLUMN_QUALIFIER",
           ["qualifierEncoded": "BASE_64_ENCODED_VALUE",]
           "fieldName": "BIGQUERY_RESULT_FIELD_NAME"
         }
       ]
    }]
   }"""
)
```

The following table describes the possible fields used in a `  bigtable_options  ` configuration:

<table>
<thead>
<tr class="header">
<th>Field name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       columnFamilies      </code></td>
<td>An array of column family descriptors.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       columnFamilies.familyId      </code></td>
<td>Identifier of Bigtable column family.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       columnFamilies.encoding      </code></td>
<td>Value can be set to <code dir="ltr" translate="no">       BINARY      </code> or <code dir="ltr" translate="no">       TEXT      </code> . For information about how types are encoded, see <a href="#bigquery_types">Supported BigQuery types</a> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       columnFamilies.columns      </code></td>
<td>An array of Bigtable column mappings.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       columnFamilies.columns.qualifierString      </code></td>
<td>Optional: A Bigtable column qualifier. Specify this value if the column qualifier has no non-UTF-8 codes. The fields <code dir="ltr" translate="no">       qualifierString      </code> and <code dir="ltr" translate="no">       qualifierEncoding      </code> are mutually exclusive. If neither <code dir="ltr" translate="no">       qualifierString      </code> nor <code dir="ltr" translate="no">       qualifierEncoded      </code> are specified, <code dir="ltr" translate="no">       fieldName      </code> is used as a column qualifier.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       columnFamilies.columns.qualifierEncoded      </code></td>
<td>Optional: Base64-encoded column qualifier. Similar to <code dir="ltr" translate="no">       qualifierString      </code> in case the column qualifier must have non-UTF-8 codes.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       columnFamilies.columns.fieldName      </code></td>
<td>Required: BigQuery result set field name. Can be an empty string in certain cases. For an example of how an empty <code dir="ltr" translate="no">       fieldName      </code> value is used with fields of simple types, see <a href="#prepare_results">Prepare query results for export</a> .</td>
</tr>
</tbody>
</table>

## Prepare query results for export

To export query results to Bigtable, the results must meet the following requirements:

  - The result set must contain a column `  rowkey  ` of the type `  STRING  ` or `  BYTES  ` .
  - Row keys, column qualifiers, values, and timestamps must not exceed Bigtable [data size limits within tables](/bigtable/quotas#limits-data-size) .
  - At least one column other than `  rowkey  ` must be present in the result set.
  - Each result set column must be of one of the [supported BigQuery types](#bigquery_types) . Any unsupported column types must be converted to one of the supported types before exporting to Bigtable.

Bigtable doesn't require column qualifiers to be valid BigQuery column names, and Bigtable supports using any bytes. For information about overriding target column qualifiers for an export, see [Configure exports with `  bigtable_options  `](#bigtable_options) .

If you use exported values with Bigtable APIs, such as [`  ReadModifyWriteRow  `](/bigtable/docs/reference/data/rpc/google.bigtable.v2#google.bigtable.v2.Bigtable.ReadModifyWriteRow) , any numerical values must use the correct [binary encoding](#bigtable_options) .

By default, standalone result columns of types other than `  STRUCT  ` or `  JSON  ` are interpreted as values for destination column families equal to result column name, and column qualifier equal to an empty string.

To demonstrate how these data types are written, consider the follow SQL example, where `  column  ` and `  column2  ` are standalone result columns:

``` text
SELECT
  x as column1, y as column2
FROM table
```

In this example query, `  SELECT x as column1  ` writes values to Bigtable under the `  column1  ` column family and `  ''  ` (empty string) column qualifier when handling types other than `  JSON  ` or `  STRUCT  ` .

You can change how these types are written in an export using the [`  bigtable_options  `](#bigtable_options) configuration, as seen in the following example:

``` text
EXPORT DATA OPTIONS (
  …
  bigtable_options="""{
   "columnFamilies" : [
      {
        "familyId": "ordered_at",
        "columns": [
           {"qualifierString": "order_time", "fieldName": ""}
        ]
      }
   ]
}"""
) AS
SELECT
  order_id as rowkey,
  STRUCT(product, amount) AS sales_info,
  EXTRACT (MILLISECOND FROM order_timestamp AT TIME ZONE "UTC") AS ordered_at
FROM T
```

In this example, BigQuery table `  T  ` contains the following row:

<table>
<thead>
<tr class="header">
<th><code dir="ltr" translate="no">       order_id      </code></th>
<th><code dir="ltr" translate="no">       order_timestamp      </code></th>
<th><code dir="ltr" translate="no">       product      </code></th>
<th><code dir="ltr" translate="no">       amount      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>101</td>
<td>2023-03-28T10:40:54Z</td>
<td>Joystick</td>
<td>2</td>
</tr>
</tbody>
</table>

If you use the preceding `  bigtable_options  ` configuration with table `  T  ` , the following data is written to Bigtable:

`  rowkey  `

`  sales_info  ` (column family)

`  ordered_at  ` (column family)

101

product

amount

order\_time

1970-01-01T00:00:00Z

Joystick

1970-01-01T00:00:00Z

2

1680000054000

`  1680000054000  ` represents `  2023-03-28T10:40:54Z  ` in milliseconds since Unix epoch time in the UTC time zone.

## Auto-create new column families

To auto-create new column families in a Bigtable table, set the [`  auto_create_column_families  ` option](/bigquery/docs/reference/standard-sql/export-statements#bigtable_export_option) in the `  EXPORT DATA  ` statement to `  true  ` . This option requires the `  bigtable.tables.update  ` permission, which is included in roles such as Bigtable Administrator ( `  roles/bigtable.admin  ` ).

``` text
EXPORT DATA OPTIONS (
uri="https://bigtable.googleapis.com/projects/PROJECT-ID/instances/INSTANCE-ID/appProfiles/APP_PROFILE_ID/tables/TABLE",
format="CLOUD_BIGTABLE",
auto_create_column_families = true
) AS
SELECT
  order_id as rowkey,
  STRUCT(product, amount) AS sales_info
FROM T
```

### Set timestamp for all cells in a row using `     _CHANGE_TIMESTAMP    `

You can add a `  _CHANGE_TIMESTAMP  ` column of the `  TIMESTAMP  ` type to the result for export. Every cell written to Bigtable uses the timestamp value from the `  _CHANGE_TIMESTAMP  ` of the exported result row.

Bigtable doesn't support timestamps earlier than Unix epoch (1970-01-01T00:00:00Z). If `  _CHANGE_TIMESTAMP  ` value is `  NULL  ` , the Unix epoch time of `  0  ` is used as the default timestamp value.

The following query writes cells for `  product  ` and `  amount  ` columns with the timestamp specified in the `  order_timestamp  ` column of table `  T  ` .

``` text
EXPORT DATA OPTIONS (...) AS
SELECT
  rowkey,
  STRUCT(product, amount) AS sales_info,
  order_timestamp as _CHANGE_TIMESTAMP
FROM T
```

## Export continuously

If you want to continually process an export query, you can configure it as a [continuous query](/bigquery/docs/continuous-queries-introduction) .

## Export multiple results with the same `     rowkey    ` value

When you export a result containing multiple rows with the same `  rowkey  ` value, values written to Bigtable end up in the same Bigtable row.

You can use this method to generate multiple versions of column values in the same row. In this example, the `  orders  ` table in BigQuery contains the following data:

<table>
<thead>
<tr class="header">
<th><code dir="ltr" translate="no">       id      </code></th>
<th><code dir="ltr" translate="no">       customer      </code></th>
<th><code dir="ltr" translate="no">       order_timestamp      </code></th>
<th><code dir="ltr" translate="no">       amount_spent      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>100</td>
<td>Bob</td>
<td>2023-01-01T10:10:54Z</td>
<td>10.99</td>
</tr>
<tr class="even">
<td>101</td>
<td>Alice</td>
<td>2023-01-02T12:10:50Z</td>
<td>102.7</td>
</tr>
<tr class="odd">
<td>102</td>
<td>Bob</td>
<td>2023-01-04T15:17:01Z</td>
<td>11.1</td>
</tr>
</tbody>
</table>

The user then executes the following `  EXPORT DATA  ` statement:

``` text
EXPORT DATA OPTIONS (
uri="https://bigtable.googleapis.com/projects/PROJECT-ID/instances/INSTANCE-ID/appProfiles/APP_PROFILE_ID/tables/TABLE",
format="CLOUD_BIGTABLE"
) AS
SELECT customer as rowkey, STRUCT(amount_spent) as orders_column_family, order_timestamp as _CHANGE_TIMESTAMP
FROM orders
```

Using this statement with the BigQuery `  orders  ` table results in the following data written to Bigtable:

orders\_column\_family

Row key

amount\_spent

Alice

2023-01-02T12:10:50Z

102.7

Bob

2023-01-01T10:10:54Z

10.99

2023-01-04T15:17:01Z

11.1

Exporting to Bigtable merges new values into the table instead of replacing entire rows. If values are already present in Bigtable for a row key, then new values can partially or fully override earlier values depending on the column family, column names, and timestamps of the cells being written.

**Caution:** Avoid exporting results that have multiple rows with different values for the same row key, column family, column qualifier, and timestamp. The outcome of such an export is non-deterministic and depends on the query plan and scheduling inside BigQuery. BigQuery cannot determine whether the value overridden during the export existed in Bigtable before export or was previously inserted by the same export process.

## Export multiple columns as Protocol Buffer (Protobuf) values

[Protocol buffers](https://protobuf.dev/) provide a flexible and efficient mechanism for serializing structured data. Exporting as a Protobuf can be beneficial considering how different types are handled between BigQuery and Bigtable. You can use BigQuery user-defined functions (UDFs) to export data as Protobuf binary values to Bigtable. For more information, see [Export data as Protobuf columns](/bigquery/docs/protobuf-export) .

## Export optimization

You can change the throughput at which records are exported from BigQuery to Bigtable by modifying the number of nodes in the [Bigtable destination cluster](/bigtable/docs/instances-clusters-nodes) . The throughput (rows written per second) linearly scales with the numbers of nodes in the destination cluster. For example, if you double the number of nodes in your destination cluster, your export throughput will roughly double.

## Pricing

When you export data in a standard query, you are billed using [data extraction pricing](https://cloud.google.com/bigquery/pricing#data_extraction_pricing) . When you export data in a continuous query, you are billed using [BigQuery capacity compute pricing](https://cloud.google.com/bigquery/pricing#capacity_compute_analysis_pricing) . To run continuous queries, you must have a [reservation](/bigquery/docs/reservations-workload-management) that uses the [Enterprise or Enterprise Plus edition](/bigquery/docs/editions-intro) , and a [reservation assignment](/bigquery/docs/reservations-workload-management#assignments) that uses the `  CONTINUOUS  ` job type.

After the data is exported, you're charged for storing the data in Bigtable. For more information, see [Bigtable pricing](https://cloud.google.com/bigtable/pricing#storage) .
