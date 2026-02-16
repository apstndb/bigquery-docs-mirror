  - [JSON representation](#SCHEMA_REPRESENTATION)
  - [Point](#Point)
      - [JSON representation](#Point.SCHEMA_REPRESENTATION)
  - [TimeInterval](#TimeInterval)
      - [JSON representation](#TimeInterval.SCHEMA_REPRESENTATION)
  - [TypedValue](#TypedValue)
      - [JSON representation](#TypedValue.SCHEMA_REPRESENTATION)

The metrics object for a SubTask.

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
  &quot;metric&quot;: string,
  &quot;valueType&quot;: enum (ValueType),
  &quot;metricKind&quot;: enum (MetricKind),
  &quot;points&quot;: [
    {
      object (Point)
    }
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  metric  `

`  string  `

Required. The name of the metric.

If the metric is not known by the service yet, it will be auto-created.

`  valueType  `

`  enum ( ValueType  ` )

Required. The value type of the time series.

`  metricKind  `

`  enum ( MetricKind  ` )

Optional. The metric kind of the time series.

If present, it must be the same as the metric kind of the associated metric. If the associated metric's descriptor must be auto-created, then this field specifies the metric kind of the new descriptor and must be either `  GAUGE  ` (the default) or `  CUMULATIVE  ` .

`  points[]  `

`  object ( Point  ` )

Required. The data points of this time series. When listing time series, points are returned in reverse time order.

When creating a time series, this field must contain exactly one point and the point's type must be the same as the value type of the associated metric. If the associated metric's descriptor must be auto-created, then the value type of the descriptor is determined by the point's type, which must be `  BOOL  ` , `  INT64  ` , `  DOUBLE  ` , or `  DISTRIBUTION  ` .

## Point

A single data point in a time series.

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
  &quot;interval&quot;: {
    object (TimeInterval)
  },
  &quot;value&quot;: {
    object (TypedValue)
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  interval  `

`  object ( TimeInterval  ` )

The time interval to which the data point applies. For `  GAUGE  ` metrics, the start time does not need to be supplied, but if it is supplied, it must equal the end time. For `  DELTA  ` metrics, the start and end time should specify a non-zero interval, with subsequent points specifying contiguous and non-overlapping intervals. For `  CUMULATIVE  ` metrics, the start and end time should specify a non-zero interval, with subsequent points specifying the same start time and increasing end times, until an event resets the cumulative value to zero and sets a new start time for the following points.

`  value  `

`  object ( TypedValue  ` )

The value of the data point.

## TimeInterval

A time interval extending just after a start time through an end time. If the start time is the same as the end time, then the interval represents a single point in time.

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
  &quot;startTime&quot;: string,
  &quot;endTime&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  startTime  `

`  string ( Timestamp  ` format)

Optional. The beginning of the time interval. The default value for the start time is the end time. The start time must not be later than the end time.

`  endTime  `

`  string ( Timestamp  ` format)

Required. The end of the time interval.

## TypedValue

A single strongly-typed value.

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

  // Union field value can be only one of the following:
  &quot;boolValue&quot;: boolean,
  &quot;int64Value&quot;: string,
  &quot;doubleValue&quot;: number,
  &quot;stringValue&quot;: string,
  &quot;distributionValue&quot;: {
    object (Distribution)
  }
  // End of list of possible types for union field value.
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `  value  ` . The typed value field. `  value  ` can be only one of the following:

`  boolValue  `

`  boolean  `

A Boolean value: `  true  ` or `  false  ` .

`  int64Value  `

`  string ( int64 format)  `

A 64-bit integer. Its range is approximately `  +/-9.2x10^18  ` .

`  doubleValue  `

`  number  `

A 64-bit double-precision floating-point number. Its magnitude is approximately `  +/-10^(+/-300)  ` and it has 16 significant digits of precision.

`  stringValue  `

`  string  `

A variable-length string value.

`  distributionValue  `

`  object ( Distribution  ` )

A distribution value.
