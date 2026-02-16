  - [Resource: Lock](#Lock)
      - [JSON representation](#Lock.SCHEMA_REPRESENTATION)
  - [Type](#Type)
  - [State](#State)
  - [Methods](#METHODS_SUMMARY)

## Resource: Lock

Represents a lock.

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
  &quot;type&quot;: enum (Type),
  &quot;state&quot;: enum (State),

  // Union field resources can be only one of the following:
  &quot;tableId&quot;: string
  // End of list of possible types for union field resources.
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  name  `

`  string  `

Output only. The resource name. Format: projects/{project\_id\_or\_number}/locations/{locationId}/catalogs/{catalogId}/databases/{databaseId}/locks/{lock\_id}

`  createTime  `

`  string ( Timestamp  ` format)

Output only. The creation time of the lock.

A timestamp in RFC3339 UTC "Zulu" format, with nanosecond resolution and up to nine fractional digits. Examples: `  "2014-10-02T15:01:23Z"  ` and `  "2014-10-02T15:01:23.045123456Z"  ` .

`  type  `

`  enum ( Type  ` )

The lock type.

`  state  `

`  enum ( State  ` )

Output only. The lock state.

Union field `  resources  ` . The resource that the lock will be created on. `  resources  ` can be only one of the following:

`  tableId  `

`  string  `

The table ID (not fully qualified name) in the same database that the lock will be created on. The table must exist.

## Type

The lock type.

Enums

`  TYPE_UNSPECIFIED  `

The type is not specified.

`  EXCLUSIVE  `

An exclusive lock prevents another lock from being created on the same resource.

## State

The lock state.

Enums

`  STATE_UNSPECIFIED  `

The state is not specified.

`  WAITING  `

Waiting to acquire the lock.

`  ACQUIRED  `

The lock has been acquired.

## Methods

### `             check           `

Checks the state of a lock specified by the lock ID.

### `             create           `

Creates a new lock.

### `             delete           `

Deletes an existing lock specified by the lock ID.

### `             list           `

List all locks in a specified database.
