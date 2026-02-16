# CONSTRAINT\_COLUMN\_USAGE view

The `  CONSTRAINT_COLUMN_USAGE  ` view contains all columns used by [constraints](/bigquery/docs/primary-foreign-keys) . For `  PRIMARY KEY  ` constraints, these are the columns from the `  KEY_COLUMN_USAGE  ` view. For `  FOREIGN KEY  ` constraints, these are the columns of the referenced tables.

## Schema

The `  INFORMATION_SCHEMA.CONSTRAINT_COLUMN_USAGE  ` view has the following schema:

<table>
<thead>
<tr class="header">
<th>Column Name</th>
<th>Data type</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">        table_catalog       </code></p></td>
<td><p><code dir="ltr" translate="no">        STRING       </code></p></td>
<td>The name of the project that contains the dataset.</td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">        table_schema       </code></p></td>
<td><p><code dir="ltr" translate="no">        STRING       </code></p></td>
<td>The name of the dataset that contains the table. Also referred to as the <code dir="ltr" translate="no">       datasetId      </code> .</td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">        table_name       </code></p></td>
<td><p><code dir="ltr" translate="no">        STRING       </code></p></td>
<td>The name of the table. Also referred to as the <code dir="ltr" translate="no">       tableId      </code> .</td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">        column_name       </code></p></td>
<td><p><code dir="ltr" translate="no">        STRING       </code></p></td>
<td>The column name.</td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">        constraint_catalog       </code></p></td>
<td><p><code dir="ltr" translate="no">        STRING       </code></p></td>
<td>The constraint project name.</td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">        constraint_schema       </code></p></td>
<td><p><code dir="ltr" translate="no">        STRING       </code></p></td>
<td>The constraint dataset name.</td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">        constraint_name       </code></p></td>
<td><p><code dir="ltr" translate="no">        STRING       </code></p></td>
<td>The constraint name. It can be the name of the primary key if the column is used by the primary key or the name of foreign key if the column is used by a foreign key.</td>
</tr>
</tbody>
</table>

For stability, we recommend that you explicitly list columns in your information schema queries instead of using a wildcard ( `  SELECT *  ` ). Explicitly listing columns prevents queries from breaking if the underlying schema changes.

## Scope and syntax

Queries against this view must include a dataset qualifier. For queries with a dataset qualifier, you must have permissions for the dataset. For more information see [Syntax](/bigquery/docs/information-schema-intro#syntax) . The following table shows the region and resource scopes for this view:

<table>
<thead>
<tr class="header">
<th>View name</th>
<th>Resource scope</th>
<th>Region scope</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       [               PROJECT_ID              .]               DATASET              .INFORMATION_SCHEMA.CONSTRAINT_COLUMN_USAGE;      </code></td>
<td>Dataset level</td>
<td>Dataset location</td>
</tr>
</tbody>
</table>

Replace the following:

  - Optional: `  PROJECT_ID  ` : the ID of your Google Cloud project. If not specified, the default project is used.

## Examples

The following query shows the constraints for a single table in a dataset:

``` text
SELECT *
FROM PROJECT_ID.DATASET.INFORMATION_SCHEMA.CONSTRAINT_COLUMN_USAGE
WHERE table_name = TABLE;
```

Replace the following:

  - `  PROJECT_ID  ` : Optional. The name of your cloud project. If not specified, this command uses the default project.
  - `  DATASET  ` : The name of your dataset.
  - `  TABLE  ` : The name of the table.

Conversely, the following query shows the constraints for all tables in a single dataset.

``` text
SELECT *
FROM PROJECT_ID.DATASET.INFORMATION_SCHEMA.CONSTRAINT_COLUMN_USAGE;
```

With existing constraints, the query results are similar to the following:

``` text
+-----+---------------------+--------------+------------+-------------+---------------------+-------------------+-------------------------+
| row |    table_catalog    | table_schema | table_name | column_name | constraint_catalog  | constraint_schema |     constraint_name     |
+-----+---------------------+--------------+------------+-------------+---------------------+-------------------+-------------------------+
|   1 | myConstraintCatalog | myDataset    | orders     | o_okey      | myConstraintCatalog | myDataset         | orders.pk$              |
|   2 | myConstraintCatalog | myDataset    | orders     | o_okey      | myConstraintCatalog | myDataset         | lineitem.lineitem_order |
+-----+---------------------+--------------+------------+-------------+---------------------+-------------------+-------------------------+
```

**Note:** `  lineitem.lineitem_order  ` is the foreign key defined in the `  lineitem  ` table.

If the table or dataset has no constraints, the query results look like this:

``` text
+-----------------------------+
| There is no data to display |
+-----------------------------+
```
