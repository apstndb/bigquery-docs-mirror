  - [Resource: Catalog](#Catalog)
      - [JSON representation](#Catalog.SCHEMA_REPRESENTATION)
  - [Methods](#METHODS_SUMMARY)

## Resource: Catalog

Catalog is the container of databases.

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
  &quot;expireTime&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  name  `

`  string  `

Output only. The resource name. Format: projects/{project\_id\_or\_number}/locations/{locationId}/catalogs/{catalogId}

`  createTime  `

`  string ( Timestamp  ` format)

Output only. The creation time of the catalog.

A timestamp in RFC3339 UTC "Zulu" format, with nanosecond resolution and up to nine fractional digits. Examples: `  "2014-10-02T15:01:23Z"  ` and `  "2014-10-02T15:01:23.045123456Z"  ` .

`  updateTime  `

`  string ( Timestamp  ` format)

Output only. The last modification time of the catalog.

A timestamp in RFC3339 UTC "Zulu" format, with nanosecond resolution and up to nine fractional digits. Examples: `  "2014-10-02T15:01:23Z"  ` and `  "2014-10-02T15:01:23.045123456Z"  ` .

`  deleteTime  `

`  string ( Timestamp  ` format)

Output only. The deletion time of the catalog. Only set after the catalog is deleted.

A timestamp in RFC3339 UTC "Zulu" format, with nanosecond resolution and up to nine fractional digits. Examples: `  "2014-10-02T15:01:23Z"  ` and `  "2014-10-02T15:01:23.045123456Z"  ` .

`  expireTime  `

`  string ( Timestamp  ` format)

Output only. The time when this catalog is considered expired. Only set after the catalog is deleted.

A timestamp in RFC3339 UTC "Zulu" format, with nanosecond resolution and up to nine fractional digits. Examples: `  "2014-10-02T15:01:23Z"  ` and `  "2014-10-02T15:01:23.045123456Z"  ` .

## Methods

### `             create           `

Creates a new catalog.

### `             delete           `

Deletes an existing catalog specified by the catalog ID.

### `             get           `

Gets the catalog specified by the resource name.

### `             list           `

List all catalogs in a specified project.
