  - [Resource: Table](#Table)
      - [JSON representation](#Table.SCHEMA_REPRESENTATION)
  - [HiveTableOptions](#HiveTableOptions)
      - [JSON representation](#HiveTableOptions.SCHEMA_REPRESENTATION)
  - [StorageDescriptor](#StorageDescriptor)
      - [JSON representation](#StorageDescriptor.SCHEMA_REPRESENTATION)
  - [SerDeInfo](#SerDeInfo)
      - [JSON representation](#SerDeInfo.SCHEMA_REPRESENTATION)
  - [Type](#Type)
  - [Methods](#METHODS_SUMMARY)

## Resource: Table

Represents a table.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;name&quot;: string,
  &quot;createTime&quot;: string,
  &quot;updateTime&quot;: string,
  &quot;deleteTime&quot;: string,
  &quot;expireTime&quot;: string,
  &quot;type&quot;: enum (Type),
  &quot;etag&quot;: string,

  // Union field options can be only one of the following:
  &quot;hiveOptions&quot;: {
    object (HiveTableOptions)
  }
  // End of list of possible types for union field options.
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  name  `

`  string  `

Output only. The resource name. Format: projects/{project\_id\_or\_number}/locations/{locationId}/catalogs/{catalogId}/databases/{databaseId}/tables/{tableId}

`  createTime  `

`  string ( Timestamp  ` format)

Output only. The creation time of the table.

A timestamp in RFC3339 UTC "Zulu" format, with nanosecond resolution and up to nine fractional digits. Examples: `  "2014-10-02T15:01:23Z"  ` and `  "2014-10-02T15:01:23.045123456Z"  ` .

`  updateTime  `

`  string ( Timestamp  ` format)

Output only. The last modification time of the table.

A timestamp in RFC3339 UTC "Zulu" format, with nanosecond resolution and up to nine fractional digits. Examples: `  "2014-10-02T15:01:23Z"  ` and `  "2014-10-02T15:01:23.045123456Z"  ` .

`  deleteTime  `

`  string ( Timestamp  ` format)

Output only. The deletion time of the table. Only set after the table is deleted.

A timestamp in RFC3339 UTC "Zulu" format, with nanosecond resolution and up to nine fractional digits. Examples: `  "2014-10-02T15:01:23Z"  ` and `  "2014-10-02T15:01:23.045123456Z"  ` .

`  expireTime  `

`  string ( Timestamp  ` format)

Output only. The time when this table is considered expired. Only set after the table is deleted.

A timestamp in RFC3339 UTC "Zulu" format, with nanosecond resolution and up to nine fractional digits. Examples: `  "2014-10-02T15:01:23Z"  ` and `  "2014-10-02T15:01:23.045123456Z"  ` .

`  type  `

`  enum ( Type  ` )

The table type.

`  etag  `

`  string  `

The checksum of a table object computed by the server based on the value of other fields. It may be sent on update requests to ensure the client has an up-to-date value before proceeding. It is only checked for update table operations.

Union field `  options  ` . Options specified for the table type. `  options  ` can be only one of the following:

`  hiveOptions  `

`  object ( HiveTableOptions  ` )

Options of a Hive table.

## HiveTableOptions

Options of a Hive table.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;parameters&quot;: {
    string: string,
    ...
  },
  &quot;tableType&quot;: string,
  &quot;storageDescriptor&quot;: {
    object (StorageDescriptor)
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  parameters  `

`  map (key: string, value: string)  `

Stores user supplied Hive table parameters.

An object containing a list of `  "key": value  ` pairs. Example: `  { "name": "wrench", "mass": "1.3kg", "count": "3" }  ` .

`  tableType  `

`  string  `

Hive table type. For example, MANAGED\_TABLE, EXTERNAL\_TABLE.

`  storageDescriptor  `

`  object ( StorageDescriptor  ` )

Stores physical storage information of the data.

## StorageDescriptor

Stores physical storage information of the data.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;locationUri&quot;: string,
  &quot;inputFormat&quot;: string,
  &quot;outputFormat&quot;: string,
  &quot;serdeInfo&quot;: {
    object (SerDeInfo)
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  locationUri  `

`  string  `

Cloud Storage folder URI where the table data is stored, starting with "gs://".

`  inputFormat  `

`  string  `

The fully qualified Java class name of the input format.

`  outputFormat  `

`  string  `

The fully qualified Java class name of the output format.

`  serdeInfo  `

`  object ( SerDeInfo  ` )

Serializer and deserializer information.

## SerDeInfo

Serializer and deserializer information.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;serializationLib&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  serializationLib  `

`  string  `

The fully qualified Java class name of the serialization library.

## Type

The table type.

Enums

`  TYPE_UNSPECIFIED  `

The type is not specified.

`  HIVE  `

Represents a table compatible with Hive Metastore tables.

## Methods

### `             create           `

Creates a new table.

### `             delete           `

Deletes an existing table specified by the table ID.

### `             get           `

Gets the table specified by the resource name.

### `             list           `

List all tables in a specified database.

### `             patch           `

Updates an existing table specified by the table ID.

### `             rename           `

Renames an existing table specified by the table ID.
