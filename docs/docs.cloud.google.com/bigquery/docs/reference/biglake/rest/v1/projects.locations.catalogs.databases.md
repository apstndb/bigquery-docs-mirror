  - [Resource: Database](#Database)
      - [JSON representation](#Database.SCHEMA_REPRESENTATION)
  - [HiveDatabaseOptions](#HiveDatabaseOptions)
      - [JSON representation](#HiveDatabaseOptions.SCHEMA_REPRESENTATION)
  - [Type](#Type)
  - [Methods](#METHODS_SUMMARY)

## Resource: Database

Database is the container of tables.

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

  // Union field options can be only one of the following:
  &quot;hiveOptions&quot;: {
    object (HiveDatabaseOptions)
  }
  // End of list of possible types for union field options.
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  name  `

`  string  `

Output only. The resource name. Format: projects/{project\_id\_or\_number}/locations/{locationId}/catalogs/{catalogId}/databases/{databaseId}

`  createTime  `

`  string ( Timestamp  ` format)

Output only. The creation time of the database.

A timestamp in RFC3339 UTC "Zulu" format, with nanosecond resolution and up to nine fractional digits. Examples: `  "2014-10-02T15:01:23Z"  ` and `  "2014-10-02T15:01:23.045123456Z"  ` .

`  updateTime  `

`  string ( Timestamp  ` format)

Output only. The last modification time of the database.

A timestamp in RFC3339 UTC "Zulu" format, with nanosecond resolution and up to nine fractional digits. Examples: `  "2014-10-02T15:01:23Z"  ` and `  "2014-10-02T15:01:23.045123456Z"  ` .

`  deleteTime  `

`  string ( Timestamp  ` format)

Output only. The deletion time of the database. Only set after the database is deleted.

A timestamp in RFC3339 UTC "Zulu" format, with nanosecond resolution and up to nine fractional digits. Examples: `  "2014-10-02T15:01:23Z"  ` and `  "2014-10-02T15:01:23.045123456Z"  ` .

`  expireTime  `

`  string ( Timestamp  ` format)

Output only. The time when this database is considered expired. Only set after the database is deleted.

A timestamp in RFC3339 UTC "Zulu" format, with nanosecond resolution and up to nine fractional digits. Examples: `  "2014-10-02T15:01:23Z"  ` and `  "2014-10-02T15:01:23.045123456Z"  ` .

`  type  `

`  enum ( Type  ` )

The database type.

Union field `  options  ` . Options specified for the database type. `  options  ` can be only one of the following:

`  hiveOptions  `

`  object ( HiveDatabaseOptions  ` )

Options of a Hive database.

## HiveDatabaseOptions

Options of a Hive database.

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
  &quot;parameters&quot;: {
    string: string,
    ...
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  locationUri  `

`  string  `

Cloud Storage folder URI where the database data is stored, starting with "gs://".

`  parameters  `

`  map (key: string, value: string)  `

Stores user supplied Hive database parameters.

An object containing a list of `  "key": value  ` pairs. Example: `  { "name": "wrench", "mass": "1.3kg", "count": "3" }  ` .

## Type

The database type.

Enums

`  TYPE_UNSPECIFIED  `

The type is not specified.

`  HIVE  `

Represents a database storing tables compatible with Hive Metastore tables.

## Methods

### `             create           `

Creates a new database.

### `             delete           `

Deletes an existing database specified by the database ID.

### `             get           `

Gets the database specified by the resource name.

### `             list           `

List all databases in a specified catalog.

### `             patch           `

Updates an existing database specified by the database ID.
