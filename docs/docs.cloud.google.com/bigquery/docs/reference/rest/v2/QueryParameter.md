  - [JSON representation](#SCHEMA_REPRESENTATION)
  - [QueryParameterType](#QueryParameterType)
      - [JSON representation](#QueryParameterType.SCHEMA_REPRESENTATION)
  - [QueryParameterValue](#QueryParameterValue)
      - [JSON representation](#QueryParameterValue.SCHEMA_REPRESENTATION)
  - [RangeValue](#RangeValue)
      - [JSON representation](#RangeValue.SCHEMA_REPRESENTATION)

A parameter given to a query.

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
  &quot;parameterType&quot;: {
    object (QueryParameterType)
  },
  &quot;parameterValue&quot;: {
    object (QueryParameterValue)
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  name  `

`  string  `

Optional. If unset, this is a positional parameter. Otherwise, should be unique within a query.

`  parameterType  `

`  object ( QueryParameterType  ` )

Required. The type of this parameter.

`  parameterValue  `

`  object ( QueryParameterValue  ` )

Required. The value of this parameter.

## QueryParameterType

The type of a query parameter.

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
  &quot;type&quot;: string,
  &quot;arrayType&quot;: {
    object (QueryParameterType)
  },
  &quot;structTypes&quot;: [
    {
      &quot;name&quot;: string,
      &quot;type&quot;: {
        object (QueryParameterType)
      },
      &quot;description&quot;: string
    }
  ],
  &quot;rangeElementType&quot;: {
    object (QueryParameterType)
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  type  `

`  string  `

Required. The top level type of this field.

`  arrayType  `

`  object ( QueryParameterType  ` )

Optional. The type of the array's elements, if this is an array.

`  structTypes[]  `

`  object  `

Optional. The types of the fields of this struct, in order, if this is a struct.

`  structTypes[].name  `

`  string  `

Optional. The name of this field.

`  structTypes[].type  `

`  object ( QueryParameterType  ` )

Required. The type of this field.

`  structTypes[].description  `

`  string  `

Optional. Human-oriented description of the field.

`  rangeElementType  `

`  object ( QueryParameterType  ` )

Optional. The element type of the range, if this is a range.

## QueryParameterValue

The value of a query parameter.

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
  &quot;value&quot;: string,
  &quot;arrayValues&quot;: [
    {
      object (QueryParameterValue)
    }
  ],
  &quot;structValues&quot;: {
    string: {
      object (QueryParameterValue)
    },
    ...
  },
  &quot;rangeValue&quot;: {
    object (RangeValue)
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  value  `

`  string  `

Optional. The value of this value, if a simple scalar type.

`  arrayValues[]  `

`  object ( QueryParameterValue  ` )

Optional. The array values, if this is an array type.

`  structValues  `

`  map (key: string, value: object ( QueryParameterValue  ` ))

The struct field values.

`  rangeValue  `

`  object ( RangeValue  ` )

Optional. The range value, if this is a range type.

## RangeValue

Represents the value of a range.

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
  &quot;start&quot;: {
    object (QueryParameterValue)
  },
  &quot;end&quot;: {
    object (QueryParameterValue)
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  start  `

`  object ( QueryParameterValue  ` )

Optional. The start value of the range. A missing value represents an unbounded start.

`  end  `

`  object ( QueryParameterValue  ` )

Optional. The end value of the range. A missing value represents an unbounded end.
