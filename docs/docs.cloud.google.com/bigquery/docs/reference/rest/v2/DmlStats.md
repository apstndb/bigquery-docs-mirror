  - [JSON representation](#SCHEMA_REPRESENTATION)
  - [DmlMode](#DmlMode)
  - [FineGrainedDmlUnusedReason](#FineGrainedDmlUnusedReason)

Detailed statistics for DML statements

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
  &quot;insertedRowCount&quot;: string,
  &quot;deletedRowCount&quot;: string,
  &quot;updatedRowCount&quot;: string,
  &quot;dmlMode&quot;: enum (DmlMode),
  &quot;fineGrainedDmlUnusedReason&quot;: enum (FineGrainedDmlUnusedReason)
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  insertedRowCount  `

`  string ( Int64Value format)  `

Output only. Number of inserted Rows. Populated by DML INSERT and MERGE statements

`  deletedRowCount  `

`  string ( Int64Value format)  `

Output only. Number of deleted Rows. populated by DML DELETE, MERGE and TRUNCATE statements.

`  updatedRowCount  `

`  string ( Int64Value format)  `

Output only. Number of updated Rows. Populated by DML UPDATE and MERGE statements.

`  dmlMode  `

`  enum ( DmlMode  ` )

Output only. DML mode used.

`  fineGrainedDmlUnusedReason  `

`  enum ( FineGrainedDmlUnusedReason  ` )

Output only. Reason for disabling fine-grained DML if applicable.

## DmlMode

Enum to specify the DML mode used.

Enums

`  DML_MODE_UNSPECIFIED  `

Default value. This value is unused.

`  COARSE_GRAINED_DML  `

Coarse-grained DML was used.

`  FINE_GRAINED_DML  `

Fine-grained DML was used.

## FineGrainedDmlUnusedReason

Reason for disabling fine-grained DML. Additional values may be added in the future.

Enums

`  FINE_GRAINED_DML_UNUSED_REASON_UNSPECIFIED  `

Default value. This value is unused.

`  MAX_PARTITION_SIZE_EXCEEDED  `

Max partition size threshold exceeded. [Fine-grained DML Limitations](https://docs.cloud.google.com/bigquery/docs/data-manipulation-language#fine-grained-dml-limitations)

`  TABLE_NOT_ENROLLED  `

The table is not enrolled for fine-grained DML.

`  DML_IN_MULTI_STATEMENT_TRANSACTION  `

The DML statement is part of a multi-statement transaction.
