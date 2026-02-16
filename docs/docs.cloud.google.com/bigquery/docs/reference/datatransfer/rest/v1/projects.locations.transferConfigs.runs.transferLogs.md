  - [Resource: TransferMessage](#TransferMessage)
      - [JSON representation](#TransferMessage.SCHEMA_REPRESENTATION)
      - [MessageSeverity](#TransferMessage.MessageSeverity)
  - [Methods](#METHODS_SUMMARY)

## Resource: TransferMessage

Represents a user facing message for a particular data transfer run.

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
  &quot;messageTime&quot;: string,
  &quot;severity&quot;: enum (MessageSeverity),
  &quot;messageText&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  messageTime  `

`  string ( Timestamp  ` format)

Time when message was logged.

`  severity  `

`  enum ( MessageSeverity  ` )

Message severity.

`  messageText  `

`  string  `

Message text.

### MessageSeverity

Represents data transfer user facing message severity.

Enums

`  MESSAGE_SEVERITY_UNSPECIFIED  `

No severity specified.

`  INFO  `

Informational message.

`  WARNING  `

Warning message.

`  ERROR  `

Error message.

## Methods

### `             list           `

Returns log messages for the transfer run.
