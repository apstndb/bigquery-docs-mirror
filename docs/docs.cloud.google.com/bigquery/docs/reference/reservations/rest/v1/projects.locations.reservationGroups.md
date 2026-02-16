  - [Resource: ReservationGroup](#ReservationGroup)
      - [JSON representation](#ReservationGroup.SCHEMA_REPRESENTATION)
  - [Methods](#METHODS_SUMMARY)

## Resource: ReservationGroup

A reservation group is a container for reservations.

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
  &quot;name&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  name  `

`  string  `

Identifier. The resource name of the reservation group, e.g., `  projects/*/locations/*/reservationGroups/team1-prod  ` . The reservationGroupId must only contain lower case alphanumeric characters or dashes. It must start with a letter and must not end with a dash. Its maximum length is 64 characters.

## Methods

### `             create           `

Creates a new reservation group.

### `             delete           `

Deletes a reservation.

### `             get           `

Returns information about the reservation group.

### `             list           `

Lists all the reservation groups for the project in the specified location.
