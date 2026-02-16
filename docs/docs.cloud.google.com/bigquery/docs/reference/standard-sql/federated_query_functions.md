GoogleSQL for BigQuery supports the following federated query functions.

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
<td><a href="/bigquery/docs/reference/standard-sql/federated_query_functions#external_query"><code dir="ltr" translate="no">        EXTERNAL_QUERY       </code></a></td>
<td>Executes a query on an external database and returns the results as a temporary table.</td>
</tr>
</tbody>
</table>

## `     EXTERNAL_QUERY    `

``` text
EXTERNAL_QUERY('connection_id', '''external_database_query'''[, 'options'])
```

**Description**

Executes a query on an external database and returns the results as a temporary table. The external database data type is converted to a [GoogleSQL data type](/bigquery/docs/reference/standard-sql/data-types#data_type_list) in the temporary result table with [these data type mappings](#data_type_mappings) .

  - `  external_database_query  ` : The query to run on the external database.

  - `  connection_id  ` : The ID of the [connection resource](/bigquery/docs/connections-api-intro) . The connection resource contains settings for the connection between the external database and BigQuery. If you don't have a default project configured, prepend the project ID to the connection ID in following format:
    
    ``` text
    projects/PROJECT_ID/locations/LOCATION/connections/CONNECTION_ID
    ```
    
    Replace the following:
    
      - PROJECT\_ID : The project ID.
      - LOCATION : The location of the connection.
      - CONNECTION\_ID : The connection ID.
    
    For example, `  projects/example-project/locations/us/connections/sql-bq  ` .
    
    **Caution:** If you have a view that's shared across multiple projects where you use `  EXTERNAL_QUERY  ` , always use the fully qualified connection ID (projects/ PROJECT\_ID /locations/ LOCATION /connections/ CONNECTION\_ID ), otherwise the wrong project might be used.

  - `  options  ` : An optional string of a JSON format map with key value pairs of option name and value (both are case sensitive).
    
    For example: `  '{"default_type_for_decimal_columns":"numeric"}'  `
    
    Supported options:
    
    <table>
    <thead>
    <tr class="header">
    <th>Option Name</th>
    <th>Description</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>"default_type_for_decimal_columns"</td>
    <td>Can be "float64", "numeric", "bignumeric" or "string". With this option, the MySQL Decimal type or PostgreSQL Numeric type will be mapped to the provided BigQuery type. When this option isn't provided, the MySQL Decimal type or PostgreSQL Numeric type will be mapped to BigQuery NUMERIC type.</td>
    </tr>
    <tr class="even">
    <td>"query_execution_priority"</td>
    <td>Can be "low", "medium" or "high". Only supported in Spanner. Specifies priority for execution of the query. Execution priority is "medium" by default.</td>
    </tr>
    </tbody>
    </table>

Additional notes:

  - The `  EXTERNAL_QUERY  ` function is usually used in a `  FROM  ` clause.
  - You can use the `  EXTERNAL_QUERY()  ` function to access metadata about the external database.
  - `  EXTERNAL_QUERY()  ` won't honor the ordering of the external query result, even if your external query includes `  ORDER BY  ` .

**Return Data Type**

BigQuery table

**Examples**

Suppose you need the date of the first order for each of your customers to include in a report. This data is not currently in BigQuery but is available in your operational PostgreSQL database in . The following federated query example accomplishes this and includes 3 parts:

1.  Run the external query `  SELECT customer_id, MIN(order_date) AS first_order_date FROM orders GROUP BY customer_id  ` in the operational PostgreSQL database to get the first order date for each customer through the `  EXTERNAL_QUERY()  ` function.
2.  Join external query result table with customers table in BigQuery by `  customer_id  ` .
3.  Select customer information and first order date.

<!-- end list -->

``` text
SELECT
  c.customer_id, c.name, SUM(t.amount) AS total_revenue, rq.first_order_date
FROM customers AS c
INNER JOIN transaction_fact AS t ON c.customer_id = t.customer_id
LEFT OUTER JOIN
  EXTERNAL_QUERY(
    'connection_id',
    '''SELECT customer_id, MIN(order_date) AS first_order_date
       FROM orders
       GROUP BY customer_id'''
  ) AS rq
  ON rq.customer_id = c.customer_id
GROUP BY c.customer_id, c.name, rq.first_order_date;
```

You can use the `  EXTERNAL_QUERY()  ` function to query information\_schema tables to access database metadata, such as list all tables in the database or show table schema. The following example information\_schema queries work in both [MySQL](https://dev.mysql.com/doc/refman/8.0/en/information-schema-introduction.html) and [PostgreSQL](https://www.postgresql.org/docs/9.1/information-schema.html) .

``` text
-- List all tables in a database.
SELECT *
FROM
  EXTERNAL_QUERY(
    'connection_id',
    '''SELECT * FROM information_schema.tables'''
  );
```

``` text
-- List all columns in a table.
SELECT *
FROM
  EXTERNAL_QUERY(
    'connection_id',
    '''SELECT * FROM information_schema.columns WHERE table_name='x';'''
  );
```

`  EXTERNAL_QUERY()  ` won't honor the ordering of the external query result, even if your external query includes `  ORDER BY  ` . The following example query orders rows by customer ID in the external database, but BigQuery will not output the result rows in that order.

``` text
-- ORDER BY will not order rows.
SELECT *
FROM
  EXTERNAL_QUERY(
    'connection_id',
    '''SELECT * FROM customers AS c ORDER BY c.customer_id'''
  );
```

#### Data type mappings

When you execute a federated query, the data from the external database are converted to GoogleSQL types. Below are the data type mappings from [MySQL to BigQuery](#mysql_mapping) and [PostgreSQL to BigQuery](#postgresql_mapping) .

Things to know about mapping:

  - Most MySQL data types can be matched to the same BigQuery data type, with a few exceptions such as `  decimal  ` , `  timestamp  ` , and `  time  ` .
  - PostgreSQL supports many non-standard data types which aren't supported in BigQuery, for example `  money  ` , `  path  ` , `  uuid  ` , `  boxer  ` , and others.
  - The numeric data types in MySQL and PostgreSQL will be mapped to BigQuery `  NUMERIC  ` value by default. The BigQuery `  NUMERIC  ` value range is smaller than in MySQL and PostgreSQL. It can also be mapped to [`  BIGNUMERIC  `](/bigquery/docs/reference/standard-sql/data-types#numeric_types) , `  FLOAT64  ` , or `  STRING  ` with ["default\_type\_for\_decimal\_columns"](#external_query_options) in `  EXTERNAL_QUERY  ` options.

**Error handling**

If your external query contains a data type that's unsupported in BigQuery, the query will fail immediately. You can cast the unsupported data type to a different MySQL / PostgreSQL data type that is supported. See [unsupported data types](#unsupported_data_types) for more information on how to cast.

#### MySQL to BigQuery type mapping

**MySQL type**

**MySQL Description**

**BigQuery type**

**Type difference**

**Integer**

INT

4 bytes, 2^32 - 1

INT64

TINYINT

1 byte, 2^8 - 1

INT64

SMALLINT

2 bytes, 2^16 - 1

INT64

MEDIUMINT

3 bytes, 2^24 - 1

INT64

BIGINT

8 bytes, 2^64 - 1

INT64

UNSIGNED BIGINT

8 bytes, 2^64 - 1

NUMERIC

**Exact numeric**

DECIMAL (M,D)

A decimal represents by (M,D) where M is the total number of digits and D is the number of decimals. M \<= 65

NUMERIC, BIGNUMERIC, FLOAT64, or STRING  
  

DECIMAL (M,D) will to mapped to NUMERIC by default, or can be mapped to BIGNUMERIC, FLOAT64, or STRING with [default\_type\_for\_decimal\_columns](#external_query_options) .

**Approximate numeric**

FLOAT (M,D)

4 bytes, M \<= 23

FLOAT64

DOUBLE (M,D)

8 bytes, M \<= 53

FLOAT64

**Date and time**

TIMESTAMP

'1970-01-01 00:00:01'UTC to '2038-01-19 03:14:07' UTC.

TIMESTAMP

MySQL TIMESTAMP is retrieved as UTC timezone no matter where user call BigQuery

DATETIME

'1000-01-01 00:00:00' to '9999-12-31 23:59:59'

DATETIME

DATE

'1000-01-01' to '9999-12-31'.

DATE

TIME

Time in 'HH:MM:SS' format  
'-838:59:59' to '838:59:59'.

TIME  

BigQuery TIME range is smaller, from 00:00:00 to 23:59:59

YEAR

INT64

**Character and strings**

ENUM

string object with a value chosen from a list of permitted values

STRING

CHAR (M)

A fixed-length string between 1 and 255 characters

STRING

VARCHAR (M)

A variable-length string between 1 and 255 characters in length.

STRING

TEXT

A field with a maximum length of 65535 characters.

STRING

TINYTEXT

TEXT column with a maximum length of 255 characters.

STRING

MEDIUMTEXT

TEXT column with a maximum length of 16777215 characters.

STRING

LONGTEXT

TEXT column with a maximum length of 4294967295 characters.

STRING

**Binary**

BLOB

A binary large object with a maximum length of 65535 characters.

BYTES

MEDIUM\_BLOB

A BLOB with a maximum length of 16777215 characters.

BYTES

LONG\_BLOB

A BLOB with a maximum length of 4294967295 characters.

BYTES

TINY\_BLOB

A BLOB with a maximum length of 255 characters.

BYTES

BINARY

A fixed-length binary string between 1 and 255 characters.

BYTES

VARBINARY

A variable-length binary string between 1 and 255 characters.

BYTES

**Other**

SET

when declare SET column, predefine some values. Then INSERT any set of predefined values into this column

STRING

GEOMETRY

GEOGRAPHY

NOT YET SUPPORTED

BIT

INT64

NOT YET SUPPORTED

#### PostgreSQL to BigQuery type mapping

<table>
<thead>
<tr class="header">
<th><strong>Name</strong></th>
<th><strong>Description</strong></th>
<th><strong>BigQuery type</strong></th>
<th><strong>Type difference</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>Integer</strong></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>smallint</td>
<td>2 bytes, -32768 to +32767</td>
<td>INT64</td>
<td></td>
</tr>
<tr class="odd">
<td>smallserial</td>
<td>See smallint</td>
<td>INT64</td>
<td></td>
</tr>
<tr class="even">
<td>integer</td>
<td>4 bytes, -2147483648 to +2147483647</td>
<td>INT64</td>
<td></td>
</tr>
<tr class="odd">
<td>serial</td>
<td>See integer</td>
<td>INT64</td>
<td></td>
</tr>
<tr class="even">
<td>bigint</td>
<td>8 bytes, -9223372036854775808 to 9223372036854775807</td>
<td>INT64</td>
<td></td>
</tr>
<tr class="odd">
<td>bigserial</td>
<td>See bigint</td>
<td>INT64</td>
<td></td>
</tr>
<tr class="even">
<td><strong>Exact numeric</strong></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td>numeric [ (p, s) ]</td>
<td>Precision up to 1,000.</td>
<td>NUMERIC, BIGNUMERIC, FLOAT64, or STRING</td>
<td>numeric [ (p, s) ] will to mapped to NUMERIC by default, or can be mapped to BIGNUMERIC, FLOAT64, or STRING with <a href="#external_query_options">default_type_for_decimal_columns</a> .</td>
</tr>
<tr class="even">
<td>Decimal [ (p, s) ]</td>
<td>See numeric</td>
<td>NUMERIC</td>
<td>See numeric</td>
</tr>
<tr class="odd">
<td>money</td>
<td>8 bytes, 2 digit scale, -92233720368547758.08 to +92233720368547758.07</td>
<td>NOT SUPPORTED</td>
<td></td>
</tr>
<tr class="even">
<td><strong>Approximate numeric</strong></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td>real</td>
<td>4 bytes, single precision floating-point number</td>
<td>FLOAT64</td>
<td></td>
</tr>
<tr class="even">
<td>double precision</td>
<td>8 bytes, double precision floating-point number</td>
<td>FLOAT64</td>
<td></td>
</tr>
<tr class="odd">
<td><strong>Date and time</strong></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>date</td>
<td>calendar date (year, month, day)</td>
<td>DATE</td>
<td></td>
</tr>
<tr class="odd">
<td>time [ (p) ] [ without time zone ]</td>
<td>time of day (no time zone)</td>
<td>TIME</td>
<td></td>
</tr>
<tr class="even">
<td>time [ (p) ] with time zone</td>
<td>time of day, including time zone</td>
<td>NOT SUPPORTED</td>
<td></td>
</tr>
<tr class="odd">
<td>timestamp [ (p) ] [ without time zone ]</td>
<td>date and time (no time zone)</td>
<td>DATETIME</td>
<td></td>
</tr>
<tr class="even">
<td>timestamp [ (p) ] with time zone</td>
<td>date and time, including time zone</td>
<td>TIMESTAMP</td>
<td>PostgreSQL TIMESTAMP is retrieved as UTC timezone no matter where user call BigQuery</td>
</tr>
<tr class="odd">
<td>interval</td>
<td>A time duration</td>
<td>NOT SUPPORTED</td>
<td></td>
</tr>
<tr class="even">
<td><strong>Character and strings</strong></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td>character [ (n) ]</td>
<td>fixed-length character string</td>
<td>STRING</td>
<td></td>
</tr>
<tr class="even">
<td>character varying [ (n) ]</td>
<td>variable-length character string</td>
<td>STRING</td>
<td></td>
</tr>
<tr class="odd">
<td>text</td>
<td>variable-length character string</td>
<td>STRING</td>
<td></td>
</tr>
<tr class="even">
<td><strong>Binary</strong></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td>bytea</td>
<td>binary data ("byte array")</td>
<td>BYTES</td>
<td></td>
</tr>
<tr class="even">
<td>bit [ (n) ]</td>
<td>fixed-length bit string</td>
<td>BYTES</td>
<td></td>
</tr>
<tr class="odd">
<td>bit varying [ (n) ]</td>
<td>variable-length bit string</td>
<td>BYTES</td>
<td></td>
</tr>
<tr class="even">
<td><strong>Other</strong></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td>boolean</td>
<td>logical Boolean (true/false)</td>
<td>BOOL</td>
<td></td>
</tr>
<tr class="even">
<td>inet</td>
<td>IPv4 or IPv6 host address</td>
<td>NOT SUPPORTED</td>
<td></td>
</tr>
<tr class="odd">
<td>path</td>
<td>geometric path on a plane</td>
<td>NOT SUPPORTED</td>
<td></td>
</tr>
<tr class="even">
<td>pg_lsn</td>
<td>PostgreSQL Log Sequence Number</td>
<td>NOT SUPPORTED</td>
<td></td>
</tr>
<tr class="odd">
<td>point</td>
<td>geometric point on a plane</td>
<td>NOT SUPPORTED</td>
<td></td>
</tr>
<tr class="even">
<td>polygon</td>
<td>closed geometric path on a plane</td>
<td>NOT SUPPORTED</td>
<td></td>
</tr>
<tr class="odd">
<td>tsquery</td>
<td>text search query</td>
<td>NOT SUPPORTED</td>
<td></td>
</tr>
<tr class="even">
<td>tsvector</td>
<td>text search document</td>
<td>NOT SUPPORTED</td>
<td></td>
</tr>
<tr class="odd">
<td>txid_snapshot</td>
<td>user-level transaction ID snapshot</td>
<td>NOT SUPPORTED</td>
<td></td>
</tr>
<tr class="even">
<td>uuid</td>
<td>universally unique identifier</td>
<td>NOT SUPPORTED</td>
<td></td>
</tr>
<tr class="odd">
<td>xml</td>
<td>XML data</td>
<td>STRING</td>
<td></td>
</tr>
<tr class="even">
<td>box</td>
<td>rectangular box on a plane</td>
<td>NOT SUPPORTED</td>
<td></td>
</tr>
<tr class="odd">
<td>cidr</td>
<td>IPv4 or IPv6 network address</td>
<td>NOT SUPPORTED</td>
<td></td>
</tr>
<tr class="even">
<td>circle</td>
<td>circle on a plane</td>
<td>NOT SUPPORTED</td>
<td></td>
</tr>
<tr class="odd">
<td>interval [ fields ] [ (p) ]</td>
<td>time span</td>
<td>NOT SUPPORTED</td>
<td></td>
</tr>
<tr class="even">
<td>json</td>
<td>textual JSON data</td>
<td>STRING</td>
<td></td>
</tr>
<tr class="odd">
<td>jsonb</td>
<td>binary JSON data, decomposed</td>
<td>NOT SUPPORTED</td>
<td></td>
</tr>
<tr class="even">
<td>line</td>
<td>infinite line on a plane</td>
<td>NOT SUPPORTED</td>
<td></td>
</tr>
<tr class="odd">
<td>lseg</td>
<td>line segment on a plane</td>
<td>NOT SUPPORTED</td>
<td></td>
</tr>
<tr class="even">
<td>macaddr</td>
<td>MAC (Media Access Control) address</td>
<td>NOT SUPPORTED</td>
<td></td>
</tr>
<tr class="odd">
<td>macaddr8</td>
<td>MAC (Media Access Control) address (EUI-64 format)</td>
<td>NOT SUPPORTED</td>
<td></td>
</tr>
</tbody>
</table>

#### Unsupported MySQL and PostgreSQL data types

If your external query contains a data type that's unsupported in BigQuery, the query will fail immediately. You can cast the unsupported data type to a different supported MySQL / PostgreSQL data type.

  - Unsupported MySQL data type
      - **Error message:** `  Invalid table-valued function external_query Found unsupported MySQL type in BigQuery. at [1:15]  `
      - **Unsupported type:** `  GEOMETRY  ` , `  BIT  `
      - **Resolution:** Cast the unsupported data type to STRING.
      - **Example:** `  SELECT ST_AsText(ST_GeomFromText('POINT(1 1)'));  ` This command casts the unsupported data type `  GEOMETRY  ` to `  STRING  ` .
  - Unsupported PostgreSQL data type
      - **Error message:** `  Invalid table-valued function external_query Postgres type (OID = 790) isn't supported now at [1:15]  `
      - **Unsupported type:** `  money, time with time zone, inet, path, pg_lsn, point, polygon, tsquery, tsvector, txid_snapshot, uuid, box, cidr, circle, interval, jsonb, line, lseg, macaddr, macaddr8  `
      - **Resolution:** Cast the unsupported data type to STRING.
      - **Example:** `  SELECT CAST('12.34'::float8::numeric::money AS varchar(30));  ` This command casts the unsupported data type `  money  ` to `  string  ` .

#### Spanner to BigQuery type mapping

When you execute a Spanner federated query, the data from Spanner is converted to GoogleSQL types.

<table>
<thead>
<tr class="header">
<th>Spanner GoogleSQL type</th>
<th>Spanner PostgreSQL type</th>
<th>BigQuery type</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       ARRAY      </code></td>
<td>-</td>
<td><code dir="ltr" translate="no">       ARRAY      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       BOOL      </code></td>
<td><code dir="ltr" translate="no">       bool      </code></td>
<td><code dir="ltr" translate="no">       BOOL      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       BYTES      </code></td>
<td><code dir="ltr" translate="no">       bytea      </code></td>
<td><code dir="ltr" translate="no">       BYTES      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       DATE      </code></td>
<td><code dir="ltr" translate="no">       date      </code></td>
<td><code dir="ltr" translate="no">       DATE      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       FLOAT64      </code></td>
<td><code dir="ltr" translate="no">       float8      </code></td>
<td><code dir="ltr" translate="no">       FLOAT64      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       INT64      </code></td>
<td><code dir="ltr" translate="no">       bigint      </code></td>
<td><code dir="ltr" translate="no">       INT64      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       JSON      </code></td>
<td><code dir="ltr" translate="no">       JSONB      </code></td>
<td><code dir="ltr" translate="no">       JSON      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       NUMERIC      </code></td>
<td><code dir="ltr" translate="no">       numeric      </code> *</td>
<td><code dir="ltr" translate="no">       NUMERIC      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td><code dir="ltr" translate="no">       varchar      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       STRUCT      </code></td>
<td>-</td>
<td>Not supported for Spanner federated queries</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td><code dir="ltr" translate="no">       timestamptz      </code></td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code> with nanoseconds truncated</td>
</tr>
</tbody>
</table>

\* PostgreSQL numeric values with a precision that's greater than the precision that BigQuery supports are rounded. Values that are larger than the maximum value generate an `  Invalid NUMERIC value  ` error.

If your external query contains a data type that's unsupported for federated queries, the query fails immediately. You can cast the unsupported data type to a supported data type.

#### SAP Datasphere to BigQuery type mapping

When you execute a [SAP Datasphere federated query](/bigquery/docs/sap-datasphere-federated-queries) , the data from SAP Datasphere is converted to the following GoogleSQL types.

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>SAP Datasphere type</strong></th>
<th><strong>SAP Datasphere description</strong></th>
<th><strong>BigQuery type</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>Integer</strong></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>Integer</td>
<td>Standard signed integer.</td>
<td>INT64</td>
</tr>
<tr class="odd">
<td>Integer64</td>
<td>Signed 64-bit integer.</td>
<td>BIGNUMERIC</td>
</tr>
<tr class="even">
<td>hana.SMALLINT</td>
<td>Signed 16-bit integer supporting the values -32,768 to 32,767.</td>
<td>INT64</td>
</tr>
<tr class="odd">
<td>hana.TINYINT</td>
<td>Unsigned 8-bit integer supporting the values 0 to 255.</td>
<td>INT64</td>
</tr>
<tr class="even">
<td><strong>Exact numeric</strong></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td>Decimal (p, s)</td>
<td>Precision (p) defines the number of total digits and can be between 1 and 38.<br />
<br />
Scale (s) defines the number of digits after the decimal point and can be between 0 and p.</td>
<td>BIGNUMERIC</td>
</tr>
<tr class="even">
<td>DecimalFloat</td>
<td>Decimal floating-point number with 34 mantissa digits.</td>
<td>BIGNUMERIC</td>
</tr>
<tr class="odd">
<td>hana.SMALLDECIMAL</td>
<td>64-bit decimal floating-point number, where (p) can be between 1 and 16 and s can be between -369 and 368.</td>
<td>BIGNUMERIC</td>
</tr>
<tr class="even">
<td><strong>Approximate numeric</strong></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td>Double</td>
<td>Double-precision, 64-bit floating-point number.</td>
<td>FLOAT64</td>
</tr>
<tr class="even">
<td>hana.REAL</td>
<td>32-bit binary floating-point number.</td>
<td>FLOAT64</td>
</tr>
<tr class="odd">
<td><strong>Date and time</strong></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>Date</td>
<td>Default format YYYY-MM-DD.</td>
<td>DATE</td>
</tr>
<tr class="odd">
<td>Datetime</td>
<td>Default format YYYY-MM-DD HH24:MI:SS.</td>
<td>TIMESTAMP</td>
</tr>
<tr class="even">
<td>Time</td>
<td>Default format HH24:MI:SS.</td>
<td>TIME</td>
</tr>
<tr class="odd">
<td>Timestamp</td>
<td>Default format YYYY-MM-DD HH24:MI:SS.</td>
<td>TIMESTAMP</td>
</tr>
<tr class="even">
<td><strong>Character and strings</strong></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td>LargeString</td>
<td>Variable length string of up to 2GB.</td>
<td>STRING</td>
</tr>
<tr class="even">
<td>String (n)</td>
<td>Variable-length Unicode string of up to 5000 characters.</td>
<td>STRING</td>
</tr>
<tr class="odd">
<td><strong>Binary</strong></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>Binary (n)</td>
<td>Variable length byte string of up to 4000 bytes.</td>
<td>BYTES</td>
</tr>
<tr class="odd">
<td>LargeBinary</td>
<td>Variable length byte string of up to 2GB.</td>
<td>BYTES</td>
</tr>
<tr class="even">
<td>hana.BINARY (n)</td>
<td>Byte string of fixed length (n).</td>
<td>STRING</td>
</tr>
<tr class="odd">
<td><strong>Other</strong></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>Boolean</td>
<td>TRUE, FALSE and UNKNOWN, where UNKNOWN is a synonym of NULL.</td>
<td>BOOL</td>
</tr>
<tr class="odd">
<td>UUID</td>
<td>Universally unique identifier encoded as a 128-bit integer.</td>
<td>STRING</td>
</tr>
<tr class="even">
<td>hana.ST_GEOMETRY</td>
<td>Spatial data in any form, including 0-dimensional points, lines, multi-lines, and polygons.</td>
<td>NOT SUPPORTED</td>
</tr>
<tr class="odd">
<td>hana.ST_POINT</td>
<td>Spatial data in the form of 0-dimensional points that represents a single location in coordinate space.</td>
<td>NOT SUPPORTED</td>
</tr>
</tbody>
</table>
