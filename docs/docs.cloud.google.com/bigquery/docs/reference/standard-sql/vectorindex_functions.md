**Preview**

This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://cloud.google.com/terms/service-terms) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products#product-launch-stages) .

**Note:** To provide feedback or request support for this feature, send email to <bq-vector-search@google.com> .

GoogleSQL for BigQuery supports the following vector index functions.

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
<td><a href="/bigquery/docs/reference/standard-sql/vectorindex_functions#vector_indexstatistics"><code dir="ltr" translate="no">        VECTOR_INDEX.STATISTICS       </code></a></td>
<td>Calculate how much an indexed table's data has drifted between when a vector index was trained and the present.</td>
</tr>
</tbody>
</table>

## `     VECTOR_INDEX.STATISTICS    `

**Preview**

This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://cloud.google.com/terms/service-terms) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products#product-launch-stages) .

**Note:** To provide feedback or request support for this feature, send email to <bq-vector-search@google.com> .

``` text
VECTOR_INDEX.STATISTICS(
  TABLE table_name
)
```

**Description**

The `  VECTOR_INDEX.STATISTICS  ` function calculates how much an indexed table's data has drifted between when a [vector index](/bigquery/docs/vector-index) was trained and the present. Use this function to determine if table data has changed enough to require a vector index rebuild. If necessary, you can use the [`  ALTER VECTOR INDEX REBUILD  ` statement](/bigquery/docs/reference/standard-sql/data-definition-language#alter_vector_index_rebuild_statement) to rebuild the vector index.

To alter vector indexes, you must have the BigQuery Data Editor ( `  roles/bigquery.dataEditor  ` ) or BigQuery Data Owner ( `  roles/bigquery.dataOwner  ` ) IAM role on the table that contains the vector index.

**Definitions**

  - `  table_name  ` : The name of the table that contains the vector index, in the format `  dataset_name.table_name  ` .
    
    If there is no active vector index on the table, the function returns empty results. If there is an active vector index on the table, but the index training isn't complete, the function returns a `  NULL  ` drift score.

**Output**

A `  FLOAT64  ` value in the range `  [0,1)  ` . A lower value indicates less drift. Typically, a change of `  0.3  ` or greater is considered significant.

**Example**

This example returns the drift for the table `  mytable  ` .

``` text
SELECT * FROM VECTOR_INDEX.STATISTICS(TABLE mydataset.mytable);
```
