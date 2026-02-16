# Impact on writes from column-level access control

This page explains the impact to writes when you use BigQuery column-level access control to restrict access to data at the column level. For general information about column-level access control, see [Introduction to BigQuery column-level access control](/bigquery/docs/column-level-security-intro) .

Column-level access control requires a user to have read permission for columns that are protected by policy tags. Some write operations need to read column data before actually writing into a column. For those operations, BigQuery checks the user's read permission to ensure the user has access to the column. For example, if a user is updating data that includes writing to a protected column, the user must have read permission for the protected column. If the user is inserting a new data row that includes writing to a protected column, the user doesn't need read access for the protected column. But, the user who writes such a row won't be able to read the newly written data unless the user has read permission for the protected columns.

The following sections provide details about different types of write operations. The examples in this topic use `  customers  ` tables with the following schema:

<table>
<thead>
<tr class="header">
<th>Field name</th>
<th>Type</th>
<th>Mode</th>
<th>Policy tag</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       user_id      </code></td>
<td>STRING</td>
<td>REQUIRED</td>
<td><code dir="ltr" translate="no">       policy-tag-1      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       credit_score      </code></td>
<td>INTEGER</td>
<td>NULLABLE</td>
<td><code dir="ltr" translate="no">       policy-tag-2      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       ssn      </code></td>
<td>STRING</td>
<td>NULLABLE</td>
<td><code dir="ltr" translate="no">       policy-tag-3      </code></td>
</tr>
</tbody>
</table>

## Using BigQuery data manipulation language (DML)

### Inserting data

For an `  INSERT  ` statement, BigQuery does not check Fine-Grained Reader permission on the policy tags on either the scanned columns or the updated columns. This is because an `  INSERT  ` does not require reading any of the column data. But, even if you successfully insert values into columns where you don't have read permission, once inserted, the values are protected as expected.

### Deleting, updating, and merging data

For `  DELETE  ` , `  UPDATE  ` , and `  MERGE  ` statements, BigQuery checks for the Fine-Grained Reader permission on the scanned columns. Columns aren't scanned by these statements unless you include a [`  WHERE  ` clause](/bigquery/docs/reference/standard-sql/query-syntax#where_clause) , or some other clause or subquery that requires the query to read data.

### Loading data

When loading data (for example, from Cloud Storage or local files) to a table, BigQuery does not check the Fine-Grained Reader permission on the columns of the destination table. This is because loading data does not require reading content from the destination table.

Streaming into BigQuery is similar to `  LOAD  ` and `  INSERT  ` . BigQuery lets you stream data into a destination table column, even if you don't have the Fine-Grained Reader permission.

### Copying data

For a copy operation, BigQuery checks whether the user has the Fine-Grained Reader permission on the source table. BigQuery does not check whether the user has the Fine-Grained Reader permission to the columns in the destination table. Like `  LOAD  ` , `  INSERT  ` , and streaming, once the copy is complete, you won't be able to read the data that was just written, unless you have the Fine-Grained Reader permission to the destination table's columns.

## DML examples

### `     INSERT    `

**Example:**

``` text
INSERT INTO customers VALUES('alice', 85, '123-456-7890');
```

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th></th>
<th>Source columns</th>
<th>Update columns</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Policy tags checked for Fine-Grained Reader?</td>
<td>N/A</td>
<td>No</td>
</tr>
<tr class="even">
<td>Columns checked</td>
<td>N/A</td>
<td><code dir="ltr" translate="no">       user_id      </code><br />
<code dir="ltr" translate="no">       credit_score      </code><br />
<code dir="ltr" translate="no">       ssn      </code></td>
</tr>
</tbody>
</table>

### `     UPDATE    `

**Example:**

``` text
UPDATE customers SET credit_score = 0
  WHERE user_id LIKE 'alice%' AND credit_score < 30
```

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th></th>
<th>Source columns</th>
<th>Update columns</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Policy tags checked for Fine-Grained Reader?</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr class="even">
<td>Columns checked</td>
<td><code dir="ltr" translate="no">       user_id      </code><br />
<code dir="ltr" translate="no">       credit_score      </code></td>
<td><code dir="ltr" translate="no">       credit_score      </code></td>
</tr>
</tbody>
</table>

### `     DELETE    `

**Example:**

``` text
DELETE customers WHERE credit_score = 0
```

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th></th>
<th>Source columns</th>
<th>Update columns</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Policy tags checked for Fine-Grained Reader?</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr class="even">
<td>Columns checked</td>
<td><code dir="ltr" translate="no">       credit_score      </code></td>
<td><code dir="ltr" translate="no">       user_id      </code><br />
<code dir="ltr" translate="no">       credit_score      </code><br />
<code dir="ltr" translate="no">       ssn      </code></td>
</tr>
</tbody>
</table>

## Load examples

### Loading from a local file or Cloud Storage

**Example:**

``` text
load --source_format=CSV samples.customers \
  ./customers_data.csv \
  ./customers_schema.json
```

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th></th>
<th>Source columns</th>
<th>Update columns</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Policy tags checked for Fine-Grained Reader?</td>
<td>N/A</td>
<td>No</td>
</tr>
<tr class="even">
<td>Columns checked</td>
<td>N/A</td>
<td><code dir="ltr" translate="no">       user_id      </code><br />
<code dir="ltr" translate="no">       credit_score      </code><br />
<code dir="ltr" translate="no">       ssn      </code></td>
</tr>
</tbody>
</table>

### Streaming

No policy tags are checked when streaming with the legacy `  insertAll  ` streaming API or the Storage Write API. For [BigQuery change data capture ingestion](/bigquery/docs/change-data-capture) , the policy tags are checked on the primary key columns.

## Copy examples

### Appending data to an existing table

**Example:**

``` text
cp -a samples.customers samples.customers_dest
```

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th></th>
<th>Source columns</th>
<th>Update columns</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Policy tags checked for Fine-Grained Reader?</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr class="even">
<td>Columns checked</td>
<td><code dir="ltr" translate="no">       customers.user_id      </code><br />
<code dir="ltr" translate="no">       customers.credit_score      </code><br />
<code dir="ltr" translate="no">       customers.ssn      </code></td>
<td><code dir="ltr" translate="no">       customers_dest.user_id      </code><br />
<code dir="ltr" translate="no">       customers_dest.credit_score      </code><br />
<code dir="ltr" translate="no">       customers_dest.ssn      </code></td>
</tr>
</tbody>
</table>

### Saving query results to a destination table

**Example:**

``` text
query --use_legacy_sql=false \
--max_rows=0 \
--destination_table samples.customers_dest \
--append_table "SELECT * FROM samples.customers LIMIT 10;"
```

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th></th>
<th>Source columns</th>
<th>Update columns</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Policy tags checked for Fine-Grained Reader?</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr class="even">
<td>Columns checked</td>
<td><code dir="ltr" translate="no">       customers.user_id      </code><br />
<code dir="ltr" translate="no">       customers.credit_score      </code><br />
<code dir="ltr" translate="no">       customers.ssn      </code></td>
<td><code dir="ltr" translate="no">       customers_dest.user_id      </code><br />
<code dir="ltr" translate="no">       customers_dest.credit_score      </code><br />
<code dir="ltr" translate="no">       customers_dest.ssn      </code></td>
</tr>
</tbody>
</table>
