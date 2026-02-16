  - [JSON representation](#SCHEMA_REPRESENTATION)
  - [Range](#Range)
      - [JSON representation](#Range.SCHEMA_REPRESENTATION)
  - [BucketOptions](#BucketOptions)
      - [JSON representation](#BucketOptions.SCHEMA_REPRESENTATION)
  - [Linear](#Linear)
      - [JSON representation](#Linear.SCHEMA_REPRESENTATION)
  - [Exponential](#Exponential)
      - [JSON representation](#Exponential.SCHEMA_REPRESENTATION)
  - [Explicit](#Explicit)
      - [JSON representation](#Explicit.SCHEMA_REPRESENTATION)
  - [Exemplar](#Exemplar)
      - [JSON representation](#Exemplar.SCHEMA_REPRESENTATION)

`  Distribution  ` contains summary statistics for a population of values. It optionally contains a histogram representing the distribution of those values across a set of buckets.

The summary statistics are the count, mean, sum of the squared deviation from the mean, the minimum, and the maximum of the set of population of values. The histogram is based on a sequence of buckets and gives a count of values that fall into each bucket. The boundaries of the buckets are given either explicitly or by formulas for buckets of fixed or exponentially increasing widths.

Although it is not forbidden, it is generally a bad idea to include non-finite values (infinities or NaNs) in the population of values, as this will render the `  mean  ` and `  sumOfSquaredDeviation  ` fields meaningless.

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
  &quot;count&quot;: string,
  &quot;mean&quot;: number,
  &quot;sumOfSquaredDeviation&quot;: number,
  &quot;range&quot;: {
    object (Range)
  },
  &quot;bucketOptions&quot;: {
    object (BucketOptions)
  },
  &quot;bucketCounts&quot;: [
    string
  ],
  &quot;exemplars&quot;: [
    {
      object (Exemplar)
    }
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  count  `

`  string ( int64 format)  `

The number of values in the population. Must be non-negative. This value must equal the sum of the values in `  bucketCounts  ` if a histogram is provided.

`  mean  `

`  number  `

The arithmetic mean of the values in the population. If `  count  ` is zero then this field must be zero.

`  sumOfSquaredDeviation  `

`  number  `

The sum of squared deviations from the mean of the values in the population. For values x\_i this is:

``` text
Sum[i=1..n]((x_i - mean)^2)
```

Knuth, "The Art of Computer Programming", Vol. 2, page 232, 3rd edition describes Welford's method for accumulating this sum in one pass.

If `  count  ` is zero then this field must be zero.

`  range  `

`  object ( Range  ` )

If specified, contains the range of the population values. The field must not be present if the `  count  ` is zero.

`  bucketOptions  `

`  object ( BucketOptions  ` )

Defines the histogram bucket boundaries. If the distribution does not contain a histogram, then omit this field.

`  bucketCounts[]  `

`  string ( int64 format)  `

The number of values in each bucket of the histogram, as described in `  bucketOptions  ` . If the distribution does not have a histogram, then omit this field. If there is a histogram, then the sum of the values in `  bucketCounts  ` must equal the value in the `  count  ` field of the distribution.

If present, `  bucketCounts  ` should contain N values, where N is the number of buckets specified in `  bucketOptions  ` . If you supply fewer than N values, the remaining values are assumed to be 0.

The order of the values in `  bucketCounts  ` follows the bucket numbering schemes described for the three bucket types. The first value must be the count for the underflow bucket (number 0). The next N-2 values are the counts for the finite buckets (number 1 through N-2). The N'th value in `  bucketCounts  ` is the count for the overflow bucket (number N-1).

`  exemplars[]  `

`  object ( Exemplar  ` )

Must be in increasing order of `  value  ` field.

## Range

The range of the population values.

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
  &quot;min&quot;: number,
  &quot;max&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  min  `

`  number  `

The minimum of the population values.

`  max  `

`  number  `

The maximum of the population values.

## BucketOptions

`  BucketOptions  ` describes the bucket boundaries used to create a histogram for the distribution. The buckets can be in a linear sequence, an exponential sequence, or each bucket can be specified explicitly. `  BucketOptions  ` does not include the number of values in each bucket.

A bucket has an inclusive lower bound and exclusive upper bound for the values that are counted for that bucket. The upper bound of a bucket must be strictly greater than the lower bound. The sequence of N buckets for a distribution consists of an underflow bucket (number 0), zero or more finite buckets (number 1 through N - 2) and an overflow bucket (number N - 1). The buckets are contiguous: the lower bound of bucket i (i \> 0) is the same as the upper bound of bucket i - 1. The buckets span the whole range of finite values: lower bound of the underflow bucket is -infinity and the upper bound of the overflow bucket is +infinity. The finite buckets are so-called because both bounds are finite.

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

  // Union field options can be only one of the following:
  &quot;linearBuckets&quot;: {
    object (Linear)
  },
  &quot;exponentialBuckets&quot;: {
    object (Exponential)
  },
  &quot;explicitBuckets&quot;: {
    object (Explicit)
  }
  // End of list of possible types for union field options.
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `  options  ` . Exactly one of these three fields must be set. `  options  ` can be only one of the following:

`  linearBuckets  `

`  object ( Linear  ` )

The linear bucket.

`  exponentialBuckets  `

`  object ( Exponential  ` )

The exponential buckets.

`  explicitBuckets  `

`  object ( Explicit  ` )

The explicit buckets.

## Linear

Specifies a linear sequence of buckets that all have the same width (except overflow and underflow). Each bucket represents a constant absolute uncertainty on the specific value in the bucket.

There are `  numFiniteBuckets + 2  ` (= N) buckets. Bucket `  i  ` has the following boundaries:

Upper bound (0 \<= i \< N-1): offset + (width \* i).

Lower bound (1 \<= i \< N): offset + (width \* (i - 1)).

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
  &quot;numFiniteBuckets&quot;: integer,
  &quot;width&quot;: number,
  &quot;offset&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  numFiniteBuckets  `

`  integer  `

Must be greater than 0.

`  width  `

`  number  `

Must be greater than 0.

`  offset  `

`  number  `

Lower bound of the first bucket.

## Exponential

Specifies an exponential sequence of buckets that have a width that is proportional to the value of the lower bound. Each bucket represents a constant relative uncertainty on a specific value in the bucket.

There are `  numFiniteBuckets + 2  ` (= N) buckets. Bucket `  i  ` has the following boundaries:

Upper bound (0 \<= i \< N-1): scale \* (growthFactor ^ i).

Lower bound (1 \<= i \< N): scale \* (growthFactor ^ (i - 1)).

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
  &quot;numFiniteBuckets&quot;: integer,
  &quot;growthFactor&quot;: number,
  &quot;scale&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  numFiniteBuckets  `

`  integer  `

Must be greater than 0.

`  growthFactor  `

`  number  `

Must be greater than 1.

`  scale  `

`  number  `

Must be greater than 0.

## Explicit

Specifies a set of buckets with arbitrary widths.

There are `  size(bounds) + 1  ` (= N) buckets. Bucket `  i  ` has the following boundaries:

Upper bound (0 \<= i \< N-1): bounds\[i\] Lower bound (1 \<= i \< N); bounds\[i - 1\]

The `  bounds  ` field must contain at least one element. If `  bounds  ` has only one element, then there are no finite buckets, and that single element is the common boundary of the overflow and underflow buckets.

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
  &quot;bounds&quot;: [
    number
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  bounds[]  `

`  number  `

The values must be monotonically increasing.

## Exemplar

Exemplars are example points that may be used to annotate aggregated distribution values. They are metadata that gives information about a particular value added to a Distribution bucket, such as a trace ID that was active when a value was added. They may contain further information, such as a example values and timestamps, origin, etc.

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
  &quot;value&quot;: number,
  &quot;timestamp&quot;: string,
  &quot;attachments&quot;: [
    {
      &quot;@type&quot;: string,
      field1: ...,
      ...
    }
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  value  `

`  number  `

Value of the exemplar point. This value determines to which bucket the exemplar belongs.

`  timestamp  `

`  string ( Timestamp  ` format)

The observation (sampling) time of the above value.

`  attachments[]  `

`  object  `

Contextual information about the example value. Examples are:

Trace: type.googleapis.com/google.monitoring.v3.SpanContext

Literal string: type.googleapis.com/google.protobuf.StringValue

Labels dropped during aggregation: type.googleapis.com/google.monitoring.v3.DroppedLabels

There may be only a single attachment of any given message type in a single exemplar, and this is enforced by the system.
