# INFORMATION\_SCHEMA.SHARED\_DATASET\_USAGE view

The `  INFORMATION_SCHEMA.SHARED_DATASET_USAGE  ` view contains the near real-time metadata about consumption of your shared dataset tables. To get started with sharing your data across organizations, see [BigQuery sharing (formerly Analytics Hub)](/bigquery/docs/analytics-hub-introduction) .

## Required roles

To get the permission that you need to query the `  INFORMATION_SCHEMA.SHARED_DATASET_USAGE  ` view, ask your administrator to grant you the [BigQuery Data Owner](/iam/docs/roles-permissions/bigquery#bigquery.dataOwner) ( `  roles/bigquery.dataOwner  ` ) IAM role on your source project. For more information about granting roles, see [Manage access to projects, folders, and organizations](/iam/docs/granting-changing-revoking-access) .

This predefined role contains the `  bigquery.datasets.listSharedDatasetUsage  ` permission, which is required to query the `  INFORMATION_SCHEMA.SHARED_DATASET_USAGE  ` view.

You might also be able to get this permission with [custom roles](/iam/docs/creating-custom-roles) or other [predefined roles](/iam/docs/roles-overview#predefined) .

## Schema

The underlying data is partitioned by the `  job_start_time  ` column and clustered by `  project_id  ` and `  dataset_id  ` .

The `  INFORMATION_SCHEMA.SHARED_DATASET_USAGE  ` has the following schema:

<table>
<thead>
<tr class="header">
<th><strong>Column name</strong></th>
<th><strong>Data type</strong></th>
<th><strong>Value</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       project_id      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td><strong>( <em>Clustering column</em> )</strong> The ID of the project that contains the shared dataset.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       dataset_id      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td><strong>( <em>Clustering column</em> )</strong> The ID of the shared dataset.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       table_id      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The ID of the accessed table.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       data_exchange_id      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The resource path of the data exchange.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       listing_id      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The resource path of the listing.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       job_start_time      </code></td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td><strong>( <em>Partitioning column</em> )</strong> The start time of this job.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       job_end_time      </code></td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td>The end time of this job.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       job_id      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The job ID. For example, <strong>bquxjob_1234</strong> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       job_project_number      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td>The number of the project this job belongs to.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       job_location      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The location of the job.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       linked_project_number      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td>The project number of the subscriber's project.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       linked_dataset_id      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The linked dataset ID of the subscriber's dataset.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       subscriber_org_number      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td>The organization number in which the job ran. This is the organization number of the subscriber. This field is empty for projects that don't have an organization.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       subscriber_org_display_name      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>A human-readable string that refers to the organization in which the job ran. This is the organization number of the subscriber. This field is empty for projects that don't have an organization.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       job_principal_subject      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The principal identifier (user email ID, service account, group email ID, domain) of users who execute jobs and queries against linked datasets.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       num_rows_processed      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td>The total number of rows processed by the base tables that are referenced by the queried resource.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       total_bytes_processed      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td>The total number of bytes processed by the base tables that are referenced by the queried resource.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       shared_resource_id      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The ID of the queried resource (table, view, or routine).</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       shared_resource_type      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The type of the queried resource. For example, <code dir="ltr" translate="no">       TABLE      </code> , <code dir="ltr" translate="no">       EXTERNAL_TABLE      </code> , <code dir="ltr" translate="no">       VIEW      </code> , <code dir="ltr" translate="no">       MATERIALIZED_VIEW      </code> , <code dir="ltr" translate="no">       TABLE_VALUED_FUNCTION      </code> , or <code dir="ltr" translate="no">       SCALAR_FUNCTION      </code> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       referenced_tables      </code></td>
<td><code dir="ltr" translate="no">       RECORD REPEATED      </code></td>
<td>Contains <code dir="ltr" translate="no">       project_id      </code> , <code dir="ltr" translate="no">       dataset_id      </code> , <code dir="ltr" translate="no">       table_id      </code> , and <code dir="ltr" translate="no">       processed_bytes      </code> fields of the base table.</td>
</tr>
</tbody>
</table>

For stability, we recommend that you explicitly list columns in your information schema queries instead of using a wildcard ( `  SELECT *  ` ). Explicitly listing columns prevents queries from breaking if the underlying schema changes.

## Data retention

The `  INFORMATION_SCHEMA.SHARED_DATASET_USAGE  ` view contains running jobs and the job history of the past 180 days.

## Scope and syntax

Queries against this view must include a [region qualifier](/bigquery/docs/information-schema-intro#syntax) . If you don't specify a regional qualifier, metadata is retrieved from the US region. The following table explains the region scope for this view:

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
<td><code dir="ltr" translate="no">       [               PROJECT_ID              .]INFORMATION_SCHEMA.SHARED_DATASET_USAGE      </code></td>
<td>Project level</td>
<td>US region</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       [               PROJECT_ID              .]`region-               REGION              `.INFORMATION_SCHEMA.SHARED_DATASET_USAGE      </code></td>
<td>Project level</td>
<td><code dir="ltr" translate="no">         REGION       </code></td>
</tr>
</tbody>
</table>

Replace the following:

  - Optional: `  PROJECT_ID  ` : the ID of your Google Cloud project. If not specified, the default project is used.
  - `  REGION  ` : any [dataset region name](/bigquery/docs/locations) . For example, ``  `region-us`  `` .
    **Note:** You must use [a region qualifier](/bigquery/docs/information-schema-intro#region_qualifier) to query `  INFORMATION_SCHEMA  ` views. The location of the query execution must match the region of the `  INFORMATION_SCHEMA  ` view.

## Examples

To run the query against a project other than your default project, add the project ID in the following format:

`  PROJECT_ID  ` . `  region-REGION_NAME  ` .INFORMATION\_SCHEMA.SHARED\_DATASET\_USAGE

For example, `  myproject.region-us.INFORMATION_SCHEMA.SHARED_DATASET_USAGE  ` .

### Get the total number of jobs executed on all shared tables

The following example calculates total jobs run by [subscribers](/bigquery/docs/analytics-hub-view-subscribe-listings) for a project:

``` text
SELECT
  COUNT(DISTINCT job_id) AS num_jobs
FROM
  `region-us`.INFORMATION_SCHEMA.SHARED_DATASET_USAGE
```

The result is similar to the following:

``` text
+------------+
| num_jobs   |
+------------+
| 1000       |
+------------+
```

To check the total jobs run by subscribers, use the `  WHERE  ` clause:

  - For datasets, use `  WHERE dataset_id = "..."  ` .
  - For tables, use `  WHERE dataset_id = "..." AND table_id = "..."  ` .

### Get the most used table based on the number of rows processed

The following query calculates the most used table based on the number of rows processed by subscribers.

``` text
SELECT
  dataset_id,
  table_id,
  SUM(num_rows_processed) AS usage_rows
FROM
  `region-us`.INFORMATION_SCHEMA.SHARED_DATASET_USAGE
GROUP BY
  1,
  2
ORDER BY
  3 DESC
LIMIT
  1
```

The output is similar to the following:

``` text
+---------------+-------------+----------------+
| dataset_id    | table_id      | usage_rows     |
+---------------+-------------+----------------+
| mydataset     | mytable     | 15             |
+---------------+-------------+----------------+
```

### Find the top organizations that consume your tables

The following query calculates the top subscribers based on the number of bytes processed from your tables. You can also use the `  num_rows_processed  ` column as a metric.

``` text
SELECT
  subscriber_org_number,
  ANY_VALUE(subscriber_org_display_name) AS subscriber_org_display_name,
  SUM(total_bytes_processed) AS usage_bytes
FROM
  `region-us`.INFORMATION_SCHEMA.SHARED_DATASET_USAGE
GROUP BY
  1
```

The output is similar to the following:

``` text
+--------------------------+--------------------------------+----------------+
|subscriber_org_number     | subscriber_org_display_name    | usage_bytes    |
+-----------------------------------------------------------+----------------+
| 12345                    | myorganization                 | 15             |
+--------------------------+--------------------------------+----------------+
```

For subscribers without an organization, you can use `  job_project_number  ` instead of `  subscriber_org_number  ` .

### Get usage metrics for your data exchange

If your [data exchange](/bigquery/docs/analytics-hub-introduction#data_exchanges) and source dataset are in different projects, follow these step to view the usage metrics for your data exchange:

1.  Find all [listings](/bigquery/docs/analytics-hub-introduction#listings) that belong to your data exchange.
2.  Retrieve the source dataset attached to the listing.
3.  To view the usage metrics for your data exchange, use the following query:

<!-- end list -->

``` text
SELECT
  *
FROM
  source_project_1.`region-us`.INFORMATION_SCHEMA.SHARED_DATASET_USAGE
WHERE
  dataset_id='source_dataset_id'
AND data_exchange_id="projects/4/locations/us/dataExchanges/x1"
UNION ALL
SELECT
  *
FROM
  source_project_2.`region-us`.INFORMATION_SCHEMA.SHARED_DATASET_USAGE
WHERE
  dataset_id='source_dataset_id'
AND data_exchange_id="projects/4/locations/us/dataExchanges/x1"
```

### Get usage metrics for shared views

The following query displays the usage metrics for all of the shared views present in a project:

``` text
SELECT
  project_id,
  dataset_id,
  table_id,
  num_rows_processed,
  total_bytes_processed,
  shared_resource_id,
  shared_resource_type,
  referenced_tables
FROM `myproject`.`region-us`.INFORMATION_SCHEMA.SHARED_DATASET_USAGE
WHERE shared_resource_type = 'VIEW'
```

The output is similar to the following:

``` text
+---------------------+----------------+----------+--------------------+-----------------------+--------------------+----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
|     project_id      |   dataset_id   | table_id | num_rows_processed | total_bytes_processed | shared_resource_id | shared_resource_type |                                                                                                              referenced_tables                                                                                                              |
+---------------------+----------------+----------+--------------------+-----------------------+--------------------+----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
|     myproject       | source_dataset | view1    |                  6 |                    38 | view1              | VIEW                 | [{"project_id":"myproject","dataset_id":"source_dataset","table_id":"test_table","processed_bytes":"21"},
{"project_id":"bq-dataexchange-exp","dataset_id":"other_dataset","table_id":"other_table","processed_bytes":"17"}]                 |

+---------------------+----------------+----------+--------------------+-----------------------+--------------------+----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
```

### Get usage metrics for shared table valued functions

The following query displays the usage metrics for all of the shared table valued functions present in a project:

``` text
SELECT
  project_id,
  dataset_id,
  table_id,
  num_rows_processed,
  total_bytes_processed,
  shared_resource_id,
  shared_resource_type,
  referenced_tables
FROM `myproject`.`region-us`.INFORMATION_SCHEMA.SHARED_DATASET_USAGE
WHERE shared_resource_type = 'TABLE_VALUED_FUNCTION'
```

The output is similar to the following:

``` text
+---------------------+----------------+----------+--------------------+-----------------------+--------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------+
|     project_id      |   dataset_id   | table_id | num_rows_processed | total_bytes_processed | shared_resource_id | shared_resource_type  |                                                  referenced_tables                                                  |
+---------------------+----------------+----------+--------------------+-----------------------+--------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------+
|     myproject       | source_dataset |          |                  3 |                    45 | provider_exp       | TABLE_VALUED_FUNCTION | [{"project_id":"myproject","dataset_id":"source_dataset","table_id":"test_table","processed_bytes":"45"}]           |
+---------------------+----------------+----------+--------------------+-----------------------+--------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------+
```
