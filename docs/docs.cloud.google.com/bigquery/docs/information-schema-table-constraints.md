# TABLE\_CONSTRAINTS view

The `  TABLE_CONSTRAINTS  ` view contains [the primary and foreign key](/bigquery/docs/primary-foreign-keys) relations in a BigQuery dataset.

## Required permissions

You need the following [Identity and Access Management (IAM) permissions](/iam/docs/overview) :

  - `  bigquery.tables.get  ` for viewing primary and foreign key definitions.
  - `  bigquery.tables.list  ` for viewing table information schemas.

Each of the following [predefined roles](/iam/docs/roles-overview#predefined) has the needed permissions to perform the workflows detailed in this document:

  - `  roles/bigquery.dataEditor  `
  - `  roles/bigquery.dataOwner  `
  - `  roles/bigquery.admin  `

**Note:** Roles are presented in ascending order of permissions granted. We recommend that you use predefined roles from earlier in the list to not allocate excess permissions.

For more information about IAM roles and permissions in BigQuery, see [Predefined roles and permissions](/bigquery/docs/access-control) .

## Schema

The `  INFORMATION_SCHEMA.TABLE_CONSTRAINTS  ` view has the following schema:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Column Name</th>
<th>Type</th>
<th>Meaning</th>
</tr>
</thead>
<tbody>
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
<td>The constraint name.</td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">        table_catalog       </code></p></td>
<td><p><code dir="ltr" translate="no">        STRING       </code></p></td>
<td>The constrained table project name.</td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">        table_schema       </code></p></td>
<td><p><code dir="ltr" translate="no">        STRING       </code></p></td>
<td>The constrained table dataset name.</td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">        table_name       </code></p></td>
<td><p><code dir="ltr" translate="no">        STRING       </code></p></td>
<td>The constrained table name.</td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">        constraint_type       </code></p></td>
<td><p><code dir="ltr" translate="no">        STRING       </code></p></td>
<td>Either <code dir="ltr" translate="no">       PRIMARY KEY      </code> or <code dir="ltr" translate="no">       FOREIGN KEY      </code> .</td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">        is_deferrable       </code></p></td>
<td><p><code dir="ltr" translate="no">        STRING       </code></p></td>
<td><code dir="ltr" translate="no">       YES      </code> or <code dir="ltr" translate="no">       NO      </code> depending on if a constraint is deferrable. Only <code dir="ltr" translate="no">       NO      </code> is supported.</td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">        initially_deferred       </code></p></td>
<td><p><code dir="ltr" translate="no">        STRING       </code></p></td>
<td>Only <code dir="ltr" translate="no">       NO      </code> is supported.</td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">        enforced       </code></p></td>
<td><p><code dir="ltr" translate="no">        STRING       </code></p></td>
<td><code dir="ltr" translate="no">       YES      </code> or <code dir="ltr" translate="no">       NO      </code> depending on if the constraint is enforced.<br />
Only <code dir="ltr" translate="no">       NO      </code> is supported.</td>
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
<td><code dir="ltr" translate="no">       [               PROJECT_ID              .]               DATASET              .INFORMATION_SCHEMA.TABLE_CONSTRAINTS;      </code></td>
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
FROM PROJECT_ID.DATASET.INFORMATION_SCHEMA.TABLE_CONSTRAINTS
WHERE table_name = TABLE;
```

Replace the following:

  - `  PROJECT_ID  ` : Optional. The name of your cloud project. If not specified, this command uses the default project.
  - `  DATASET  ` : The name of your dataset.
  - `  TABLE  ` : The name of the table.

Conversely, the following query shows the constraints for all tables in a single dataset.

``` text
SELECT *
FROM PROJECT_ID.DATASET.INFORMATION_SCHEMA.TABLE_CONSTRAINTS;
```

With existing constraints, the query results are similar to the following:

``` text
+-----+---------------------+-------------------+-----------------------+---------------------+--------------+------------+-----------------+---------------+--------------------+----------+
| Row | constraint_catalog  | constraint_schema |    constraint_name    |    table_catalog    | table_schema | table_name | constraint_type | is_deferrable | initially_deferred | enforced |
+-----+---------------------+-------------------+-----------------------+---------------------+--------------+------------+-----------------+---------------+--------------------+----------+
|   1 | myConstraintCatalog | myDataset         | orders.pk$            | myConstraintCatalog | myDataset    | orders     | PRIMARY KEY     | NO            | NO                 | NO       |
|   2 | myConstraintCatalog | myDataset         | orders.order_customer | myConstraintCatalog | myDataset    | orders     | FOREIGN KEY     | NO            | NO                 | NO       |
+-----+---------------------+-------------------+-----------------------+---------------------+--------------+------------+-----------------+---------------+--------------------+----------+
```

If the table or dataset has no constraints, the query results look like this:

``` text
+-----------------------------+
| There is no data to display |
+-----------------------------+
```
