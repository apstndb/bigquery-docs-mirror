  - [Resource: DataExchange](#DataExchange)
      - [JSON representation](#DataExchange.SCHEMA_REPRESENTATION)
  - [Methods](#METHODS_SUMMARY)

## Resource: DataExchange

A data exchange is a container that lets you share data. Along with the descriptive information about the data exchange, it contains listings that reference shared datasets.

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
  &quot;displayName&quot;: string,
  &quot;description&quot;: string,
  &quot;primaryContact&quot;: string,
  &quot;documentation&quot;: string,
  &quot;listingCount&quot;: integer,
  &quot;icon&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  name  `

`  string  `

Output only. The resource name of the data exchange. e.g. `  projects/myproject/locations/us/dataExchanges/123  ` .

`  displayName  `

`  string  `

Required. Human-readable display name of the data exchange. The display name must contain only Unicode letters, numbers (0-9), underscores (\_), dashes (-), spaces ( ), ampersands (&) and must not start or end with spaces. Default value is an empty string. Max length: 63 bytes.

`  description  `

`  string  `

Optional. Description of the data exchange. The description must not contain Unicode non-characters as well as C0 and C1 control codes except tabs (HT), new lines (LF), carriage returns (CR), and page breaks (FF). Default value is an empty string. Max length: 2000 bytes.

`  primaryContact  `

`  string  `

Optional. Email or URL of the primary point of contact of the data exchange. Max Length: 1000 bytes.

`  documentation  `

`  string  `

Optional. Documentation describing the data exchange.

`  listingCount  `

`  integer  `

Output only. Number of listings contained in the data exchange.

`  icon  `

`  string ( bytes format)  `

Optional. Base64 encoded image representing the data exchange. Max Size: 3.0MiB Expected image dimensions are 512x512 pixels, however the API only performs validation on size of the encoded data. Note: For byte fields, the content of the fields are base64-encoded (which increases the size of the data by 33-36%) when using JSON on the wire.

A base64-encoded string.

## Methods

### `             create           `

Creates a new data exchange.

### `             delete           `

Deletes an existing data exchange.

### `             get           `

Gets the details of a data exchange.

### `             getIamPolicy           `

Gets the IAM policy.

### `             list           `

Lists all data exchanges in a given project and location.

### `             patch           `

Updates an existing data exchange.

### `             setIamPolicy           `

Sets the IAM policy.

### `             testIamPermissions           `

Returns the permissions that a caller has.
