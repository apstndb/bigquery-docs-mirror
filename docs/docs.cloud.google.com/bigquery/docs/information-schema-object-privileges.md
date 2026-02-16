# OBJECT\_PRIVILEGES view

**Preview**

This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

The `  INFORMATION_SCHEMA.OBJECT_PRIVILEGES  ` view contains metadata about access control bindings that are explicitly set on BigQuery objects. This view does not contain metadata about the inherited access control bindings.

## Required permissions

To query the `  INFORMATION_SCHEMA.OBJECT_PRIVILEGES  ` view, you need following Identity and Access Management (IAM) permissions:

  - `  bigquery.datasets.get  ` for datasets.
  - `  bigquery.tables.getIamPolicy  ` for tables and views.

For more information about BigQuery permissions, see [Access control with IAM](/bigquery/docs/access-control) .

## Schema

When you query the `  INFORMATION_SCHEMA.OBJECT_PRIVILEGES  ` view, the query results contain one row for each access control binding for a resource.

The `  INFORMATION_SCHEMA.OBJECT_PRIVILEGES  ` view has the following schema:

<table>
<thead>
<tr class="header">
<th>Column name</th>
<th>Data type</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       object_catalog      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The project ID of the project that contains the resource.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       object_schema      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The name of the dataset that contains the resource. This is <code dir="ltr" translate="no">       NULL      </code> if the resource itself is a dataset.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       object_name      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The name of the table, view, or dataset the policy applies to.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       object_type      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The resource type, such as <code dir="ltr" translate="no">       SCHEMA      </code> (dataset), <code dir="ltr" translate="no">       TABLE      </code> , <code dir="ltr" translate="no">       VIEW      </code> , and <code dir="ltr" translate="no">       EXTERNAL      </code> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       privilege_type      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The role ID, such as <code dir="ltr" translate="no">       roles/bigquery.dataEditor      </code> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       grantee      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The user type and user that the role is granted to.</td>
</tr>
</tbody>
</table>

For stability, we recommend that you explicitly list columns in your information schema queries instead of using a wildcard ( `  SELECT *  ` ). Explicitly listing columns prevents queries from breaking if the underlying schema changes.

## Scope and syntax

Queries against this view must include a [region qualifier](/bigquery/docs/information-schema-intro#syntax) . A project ID is optional. If no project ID is specified, then the project that the query runs in is used. The following table explains the region scope for this view:

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
<td><code dir="ltr" translate="no">       [               PROJECT_ID              .]`region-               REGION              `.INFORMATION_SCHEMA.OBJECT_PRIVILEGES      </code></td>
<td>Project level</td>
<td><code dir="ltr" translate="no">         REGION       </code></td>
</tr>
</tbody>
</table>

Replace the following:

  - Optional: `  PROJECT_ID  ` : the ID of your Google Cloud project. If not specified, the default project is used.
  - `  REGION  ` : any [dataset region name](/bigquery/docs/locations) . For example, ``  `region-us`  `` .
    **Note:** You must use [a region qualifier](/bigquery/docs/information-schema-intro#region_qualifier) to query `  INFORMATION_SCHEMA  ` views. The location of the query execution must match the region of the `  INFORMATION_SCHEMA  ` view.

**Example**

``` text
-- Returns metadata for the access control bindings for mydataset.
SELECT * FROM myproject.`region-us`.INFORMATION_SCHEMA.OBJECT_PRIVILEGES
WHERE object_name = "mydataset";
```

## Limitations

  - `  OBJECT_PRIVILEGES  ` queries must contain a `  WHERE  ` clause limiting queries to a single dataset, table, or view.
  - Queries to retrieve access control metadata for a dataset must specify the `  object_name  ` .
  - Queries to retrieve access control metadata for a table or view must specify both `  object_name  ` AND `  object_schema  ` .

## Examples

The following example retrieves all columns from the `  INFORMATION_SCHEMA.OBJECT_PRIVILEGES  ` view.

To run the query against a project other than the project that the query is running in, add the project ID to the region in the following format: ``  ` project_id `.` region_id `.INFORMATION_SCHEMA.OBJECT_PRIVILEGES  `` .

The following example gets all access control metadata for the `  mydataset  ` dataset in the `  mycompany  ` project:

``` text
SELECT *
FROM mycompany.`region-us`.INFORMATION_SCHEMA.OBJECT_PRIVILEGES
WHERE object_name = "mydataset"
```

The results should look like the following:

``` text
  +----------------+---------------+-------------+-------------+---------------------------+-----------------------------------+
  | object_catalog | object_schema | object_name | object_type |  privilege_type           | grantee                           |
  +----------------+---------------+-------------+-------------+---------------------------+-----------------------------------+
  | mycompany      | NULL          | mydataset   | SCHEMA      | roles/bigquery.dataEditor | projectEditor:mycompany           |
  +----------------+---------------+-------------+-------------+---------------------------+-----------------------------------+
  | mycompany      | NULL          | mydataset   | SCHEMA      | roles/bigquery.dataOwner  | projectOwner:mycompany            |
  +----------------+---------------+-------------+-------------+---------------------------+-----------------------------------+
  | mycompany      | NULL          | mydataset   | SCHEMA      | roles/bigquery.dataOwner  | user:cloudysanfrancisco@gmail.com |
  +----------------+---------------+-------------+-------------+---------------------------+-----------------------------------+
  | mycompany      | NULL          | mydataset   | SCHEMA      | roles/bigquery.dataViwer  | projectViewer:mycompany           |
  +----------------+---------------+-------------+-------------+---------------------------+-----------------------------------+
  
```

The following example gets all access control information for the `  testdata  ` table in the `  mydataset  ` dataset:

``` text
SELECT *
FROM mycompany.`region-us`.INFORMATION_SCHEMA.OBJECT_PRIVILEGES
WHERE object_schema = "mydataset" AND object_name = "testdata"
```

The results should look like the following:

``` text
  +----------------+---------------+--------------+-------------+----------------------+------------------------------------+
  | object_catalog | object_schema |  object_name | object_type |  privilege_type      | grantee                            |
  +----------------+---------------+--------------+-------------+----------------------+------------------------------------+
  | mycompany      | mydataset     | testdata     | TABLE       | roles/bigquery.admin | user:baklavainthebalkans@gmail.com |
  +----------------+---------------+--------------+-------------+----------------------+------------------------------------+
  
```

The `  INFORMATION_SCHEMA.OBJECT_PRIVILEGES  ` view only shows access control bindings that are explicitly set. The first example shows that the user `  cloudysanfrancisco@gmail.com  ` has the `  bigquery.dataOwner  ` role on the `  mydataset  ` dataset. The user `  cloudysanfrancisco@gmail.com  ` inherits permissions to create, update, and delete tables in `  mydataset  ` , including the `  testdata  ` table. However, since those permissions were not explicitly granted on the `  testdata  ` table, they don't appear in the results of the second example.
