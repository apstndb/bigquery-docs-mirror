GoogleSQL for BigQuery supports the following utility functions.

## Function list

<table>
<thead>
<tr class="header">
<th>Name</th>
<th>Summary</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/utility-functions#generate_uuid"><code dir="ltr" translate="no">        GENERATE_UUID       </code></a></td>
<td>Produces a random universally unique identifier (UUID) as a <code dir="ltr" translate="no">       STRING      </code> value.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/utility-functions#typeof"><code dir="ltr" translate="no">        TYPEOF       </code></a></td>
<td>Gets the name of the data type for an expression.</td>
</tr>
</tbody>
</table>

## `     GENERATE_UUID    `

``` text
GENERATE_UUID()
```

**Description**

Returns a random universally unique identifier (UUID) as a `  STRING  ` . The returned `  STRING  ` consists of 32 hexadecimal digits in five groups separated by hyphens in the form 8-4-4-4-12. The hexadecimal digits represent 122 random bits and 6 fixed bits, in compliance with [RFC 4122 section 4.4](https://tools.ietf.org/html/rfc4122#section-4.4) . The returned `  STRING  ` is lowercase.

**Return Data Type**

STRING

**Example**

The following query generates a random UUID.

``` text
SELECT GENERATE_UUID() AS uuid;

/*--------------------------------------+
 | uuid                                 |
 +--------------------------------------+
 | 4192bff0-e1e0-43ce-a4db-912808c32493 |
 +--------------------------------------*/
```

## `     TYPEOF    `

``` text
TYPEOF(expression)
```

**Description**

Takes an expression and gets the name of the data type for that expression.

**Return type**

`  STRING  `

**Examples**

The following example produces the name of the data type for the expression passed into the `  TYPEOF  ` function. When `  NULL  ` is passed in, the [supertype](/bigquery/docs/reference/standard-sql/conversion_rules#supertypes) , `  INT64  ` , is produced.

``` text
SELECT
  TYPEOF(NULL) AS A,
  TYPEOF('hello') AS B,
  TYPEOF(12+1) AS C,
  TYPEOF(4.7) AS D

/*-------+--------+-------+--------+
 | A     | B      | C     | D      |
 +-------+--------+-------+--------+
 | INT64 | STRING | INT64 | FLOAT64 |
 +-------+--------+-------+--------*/
```

The following example produces the name of the data type for field `  y  ` in a struct.

``` text
SELECT
  TYPEOF(STRUCT<x INT64, y STRING>(25, 'apples')) AS struct_type,
  TYPEOF(STRUCT<x INT64, y STRING>(25, 'apples').y) AS field_type;

/*---------------------------+------------+
 | struct_type               | field_type |
 +---------------------------+------------+
 | STRUCT<x INT64, y STRING> | STRING     |
 +---------------------------+------------*/
```

The following example produces the name of the data type for elements in an array.

``` text
SELECT
  TYPEOF(ARRAY<INT64>[25, 32]) AS array_type,
  TYPEOF(ARRAY<INT64>[25, 32][0]) AS element_type;

/*--------------+--------------+
 | array_type   | element_type |
 +--------------+--------------+
 | ARRAY<INT64> | INT64        |
 +--------------+--------------*/
```
