# SCHEMATA view

The `  INFORMATION_SCHEMA.SCHEMATA  ` view provides information about the datasets in a project or region. The view returns one row for each dataset.

## Before you begin

To query the `  SCHEMATA  ` view for dataset metadata, you need the `  bigquery.datasets.get  ` Identity and Access Management (IAM) permission at the project level.

Each of the following predefined IAM roles includes the permissions that you need in order to get the `  SCHEMATA  ` view:

  - `  roles/bigquery.admin  `
  - `  roles/bigquery.dataEditor  `
  - `  roles/bigquery.dataOwner  `
  - `  roles/bigquery.dataViewer  `

For more information about BigQuery permissions, see [Access control with IAM](/bigquery/docs/access-control) .

## Schema

When you query the `  INFORMATION_SCHEMA.SCHEMATA  ` view, the query results contain one row for each dataset in the specified project.

The `  INFORMATION_SCHEMA.SCHEMATA  ` view has the following schema:

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
<td><code dir="ltr" translate="no">       catalog_name      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The name of the project that contains the dataset</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       schema_name      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The dataset's name also referred to as the <code dir="ltr" translate="no">       datasetId      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       schema_owner      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The value is always <code dir="ltr" translate="no">       NULL      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       creation_time      </code></td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td>The dataset's creation time</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       last_modified_time      </code></td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td>The dataset's last modified time</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       location      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The dataset's geographic location</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       ddl      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The <code dir="ltr" translate="no">         CREATE SCHEMA       </code> DDL statement that can be used to create the dataset</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       default_collation_name      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The name of the default <a href="/bigquery/docs/reference/standard-sql/collation-concepts">collation specification</a> if it exists; otherwise, <code dir="ltr" translate="no">       NULL      </code> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       sync_status      </code></td>
<td><code dir="ltr" translate="no">       JSON      </code></td>
<td>The status of the sync between the primary and secondary replicas for <a href="/bigquery/docs/data-replication">cross-region replication</a> and <a href="/bigquery/docs/managed-disaster-recovery">disaster recovery</a> datasets. Returns <code dir="ltr" translate="no">       NULL      </code> if the replica is a primary replica or the dataset doesn't use replication.</td>
</tr>
</tbody>
</table>

For stability, we recommend that you explicitly list columns in your information schema queries instead of using a wildcard ( `  SELECT *  ` ). Explicitly listing columns prevents queries from breaking if the underlying schema changes.

## Scope and syntax

Queries against this view must include a [region qualifier](/bigquery/docs/information-schema-intro#syntax) . If you do not specify a regional qualifier, metadata is retrieved from the US region. The following table explains the region scope for this view:

<table>
<thead>
<tr class="header">
<th>View Name</th>
<th>Resource scope</th>
<th>Region scope</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       [               PROJECT_ID              .]INFORMATION_SCHEMA.SCHEMATA      </code></td>
<td>Project level</td>
<td>US region</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       [               PROJECT_ID              .]`region-               REGION              `.INFORMATION_SCHEMA.SCHEMATA      </code></td>
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
-- Returns metadata for datasets in a region.
SELECT * FROM region-us.INFORMATION_SCHEMA.SCHEMATA;
```

## Example

To run the query against a project other than your default project, add the project ID to the dataset in the following format:

``` text
`PROJECT_ID`.INFORMATION_SCHEMA.SCHEMATA
```

for example, ``  `myproject`.INFORMATION_SCHEMA.SCHEMATA  `` .

``` text
SELECT
  * EXCEPT (schema_owner)
FROM
  INFORMATION_SCHEMA.SCHEMATA;
```

**Note:** `  INFORMATION_SCHEMA  ` view names are case-sensitive.

The result is similar to the following. For readability, some columns are excluded from the result.

``` text
+----------------+---------------+---------------------+---------------------+------------+------------------------------------------+
|  catalog_name  |  schema_name  |    creation_time    | last_modified_time  |  location  |                   ddl                    |
+----------------+---------------+---------------------+---------------------+------------+------------------------------------------+
| myproject      | mydataset1    | 2018-11-07 19:50:24 | 2018-11-07 19:50:24 | US         | CREATE SCHEMA `myproject.mydataset1`     |
|                |               |                     |                     |            | OPTIONS(                                 |
|                |               |                     |                     |            |   location="us"                          |
|                |               |                     |                     |            | );                                       |
+----------------+---------------+---------------------+---------------------+------------+------------------------------------------+
| myproject      | mydataset2    | 2018-07-16 04:24:22 | 2018-07-16 04:24:22 | US         | CREATE SCHEMA `myproject.mydataset2`     |
|                |               |                     |                     |            | OPTIONS(                                 |
|                |               |                     |                     |            |   default_partition_expiration_days=3.0, |
|                |               |                     |                     |            |   location="us"                          |
|                |               |                     |                     |            | );                                       |
+----------------+---------------+---------------------+---------------------+------------+------------------------------------------+
| myproject      | mydataset3    | 2018-02-07 21:08:45 | 2018-05-01 23:32:53 | US         | CREATE SCHEMA `myproject.mydataset3`     |
|                |               |                     |                     |            | OPTIONS(                                 |
|                |               |                     |                     |            |   description="My dataset",              |
|                |               |                     |                     |            |   location="us"                          |
|                |               |                     |                     |            | );                                       |
+----------------+---------------+---------------------+---------------------+------------+------------------------------------------+
```
