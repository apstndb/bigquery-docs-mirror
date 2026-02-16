# SCHEMATA\_REPLICAS view

The `  INFORMATION_SCHEMA.SCHEMATA_REPLICAS  ` view contains information about schemata replicas.

## Required role

To get the permissions that you need to query the `  INFORMATION_SCHEMA.SCHEMATA_REPLICAS  ` view, ask your administrator to grant you the [BigQuery Data Viewer](/iam/docs/roles-permissions/bigquery#bigquery.dataViewer) ( `  roles/bigquery.dataViewer  ` ) IAM role on the project. For more information about granting roles, see [Manage access to projects, folders, and organizations](/iam/docs/granting-changing-revoking-access) .

You might also be able to get the required permissions through [custom roles](/iam/docs/creating-custom-roles) or other [predefined roles](/iam/docs/roles-overview#predefined) .

## Schema

The `  INFORMATION_SCHEMA.SCHEMATA_REPLICAS  ` view contains information about dataset replicas. The `  INFORMATION_SCHEMA.SCHEMATA_REPLICAS  ` view has the following schema:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Column</th>
<th>Type</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       catalog_name      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The project ID of the project that contains the dataset.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       schema_name      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The dataset ID of the dataset.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       replica_name      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The name of the replica.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       location      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The region or multi-region the replica was created in.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       replica_primary_assigned      </code></td>
<td><code dir="ltr" translate="no">       BOOL      </code></td>
<td>If the value is <code dir="ltr" translate="no">       TRUE      </code> , the replica has the primary assignment. When you change a secondary replica to a primary, this state takes effect immediately.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       replica_primary_assignment_complete      </code></td>
<td><code dir="ltr" translate="no">       BOOL      </code></td>
<td>If the value is <code dir="ltr" translate="no">       TRUE      </code> , the primary assignment is complete. If the value is <code dir="ltr" translate="no">       FALSE      </code> , the replica is not (yet) the primary replica, even if <code dir="ltr" translate="no">       replica_primary_assigned      </code> equals <code dir="ltr" translate="no">       TRUE      </code> . For information about how long it takes for a secondary replica to become a primary, see <a href="/bigquery/docs/data-replication#promote_the_secondary_replica">Promote the secondary replica</a> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       creation_time      </code></td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td>The replica's creation time. When the replica is first created, it is not fully synced with the primary replica until <code dir="ltr" translate="no">       creation_complete      </code> equals <code dir="ltr" translate="no">       TRUE      </code> . The value of <code dir="ltr" translate="no">       creation_time      </code> is set before <code dir="ltr" translate="no">       creation_complete      </code> equals <code dir="ltr" translate="no">       TRUE      </code> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       creation_complete      </code></td>
<td><code dir="ltr" translate="no">       BOOL      </code></td>
<td>If the value is <code dir="ltr" translate="no">       TRUE      </code> , the initial full sync of the primary replica to the secondary replica is complete.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       replication_time      </code></td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td><p>The value for <code dir="ltr" translate="no">        replication_time       </code> indicates the staleness of the dataset.</p>
<p>Some tables in the replica might be ahead of this timestamp. This value is only visible in the secondary region.</p>
<p>If the dataset contains a table with streaming data, the value of <code dir="ltr" translate="no">        replication_time       </code> will not be accurate.</p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       sync_status      </code></td>
<td><code dir="ltr" translate="no">       JSON      </code></td>
<td>The status of the sync between the primary and secondary replicas for <a href="/bigquery/docs/data-replication">cross-region replication</a> and <a href="/bigquery/docs/managed-disaster-recovery">disaster recovery</a> datasets. Returns <code dir="ltr" translate="no">       NULL      </code> if the replica is a primary replica or the dataset doesn't use replication.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       replica_primary_assignment_time      </code></td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td>The time at which the primary switch to the replica was triggered.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       replica_primary_assignment_completion_time      </code></td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td>The time at which the primary switch to the replica was completed.</td>
</tr>
</tbody>
</table>

For stability, we recommend that you explicitly list columns in your information schema queries instead of using a wildcard ( `  SELECT *  ` ). Explicitly listing columns prevents queries from breaking if the underlying schema changes.

## Scope and syntax

Queries against this view must include a [region qualifier](/bigquery/docs/information-schema-intro#syntax) . The following table explains the region scope for this view:

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
<td><code dir="ltr" translate="no">       [               PROJECT_ID              .]`region-               REGION              `.INFORMATION_SCHEMA.SCHEMATA_REPLICAS[_BY_PROJECT]      </code></td>
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

This section lists example queries of the `  INFORMATION_SCHEMA.SCHEMATA_REPLICAS  ` view.

**Example: List all replicated datasets in a region**

The following example lists all the replicated datasets in the `  US  ` region:

``` text
SELECT * FROM `region-us`.INFORMATION_SCHEMA.SCHEMATA_REPLICAS;
```

The result is similar to the following:

``` text
+---------------------+-------------------+--------------+----------+--------------------------+-------------------------------------+---------------------+-------------------+------------------+
|    catalog_name     |    schema_name    | replica_name | location | replica_primary_assigned | replica_primary_assignment_complete |    creation_time    | creation_complete | replication_time |
+---------------------+-------------------+--------------+----------+--------------------------+-------------------------------------+---------------------+-------------------+------------------+
| myproject           | replica1          | us-east7     | us-east7 |                     true |                                true | 2023-04-17 20:42:45 |              true |             NULL |
| myproject           | replica1          | us-east4     | us-east4 |                    false |                               false | 2023-04-17 20:44:26 |              true |             NULL |
+---------------------+-------------------+--------------+----------+--------------------------+-------------------------------------+---------------------+-------------------+------------------+
```

**Example: List replicated datasets and the primary replica for each**

The following example lists all replicated datasets and their primary replica in the `  US  ` region:

``` text
SELECT
 catalog_name,
 schema_name,
 replica_name AS primary_replica_name,
 location AS primary_replica_location,
 replica_primary_assignment_complete AS is_primary,
FROM
 `region-us`.INFORMATION_SCHEMA.SCHEMATA_REPLICAS
WHERE
 replica_primary_assignment_complete = TRUE
 AND replica_primary_assigned = TRUE;
```

The result is similar to the following:

``` text
+---------------------+-------------+----------------------+--------------------------+------------+
|    catalog_name     | schema_name | primary_replica_name | primary_replica_location | is_primary |
+---------------------+-------------+----------------------+--------------------------+------------+
| myproject           | my_schema1  | us-east4             | us-east4                 |       true |
| myproject           | my_schema2  | us                   | US                       |       true |
| myproject           | my_schema2  | us                   | US                       |       true |
+---------------------+-------------+----------------------+--------------------------+------------+
```

**Example: List replicated datasets and their replica states**

The following example lists all replicated datasets and their replica states:

``` text
SELECT
  catalog_name,
  schema_name,
  replica_name,
  CASE
    WHEN (replica_primary_assignment_complete = TRUE AND replica_primary_assigned = TRUE) THEN 'PRIMARY'
    WHEN (replica_primary_assignment_complete = FALSE
    AND replica_primary_assigned = FALSE) THEN 'SECONDARY'
  ELSE
  'PENDING'
END
  AS replica_state,
FROM
  `region-us`.INFORMATION_SCHEMA.SCHEMATA_REPLICAS;
```

The result is similar to the following:

``` text
+---------------------+-------------+--------------+---------------+
|    catalog_name     | schema_name | replica_name | replica_state |
+---------------------+-------------+--------------+---------------+
| myproject           | my_schema1  | us-east4     | PRIMARY       |
| myproject           | my_schema1  | my_replica   | SECONDARY     |
+---------------------+-------------+--------------+---------------+
```

**Example: List when each replica was created and whether the initial backfill is complete**

The following example lists all replicas and when that replica was created. When a secondary replica is created, its data is not fully synced with the primary replica until `  creation_complete  ` equals `  TRUE  ` .

``` text
SELECT
 catalog_name,
 schema_name,
 replica_name,
 creation_time AS creation_time,
FROM
 `region-us`.INFORMATION_SCHEMA.SCHEMATA_REPLICAS
WHERE
 creation_complete = TRUE;
```

The result is similar to the following:

``` text
+---------------------+-------------+--------------+---------------------+
|    catalog_name     | schema_name | replica_name |    creation_time    |
+---------------------+-------------+--------------+---------------------+
| myproject           | my_schema1  | us-east4     | 2023-06-15 00:09:11 |
| myproject           | my_schema2  | us           | 2023-06-15 00:19:27 |
| myproject           | my_schema2  | my_replica2  | 2023-06-15 00:19:50 |
| myproject           | my_schema1  | my_replica   | 2023-06-15 00:16:19 |
+---------------------+-------------+--------------+---------------------+
```

**Example: Show the most recent synced time**

The following example shows the most recent timestamp when the secondary replica caught up with the primary replica.

You must run this query in the region that contains the secondary replica. Some tables in the dataset might be ahead of the reported replication time.

``` text
SELECT
 catalog_name,
 schema_name,
 replica_name,
 -- Calculate the replication lag in seconds.
 TIMESTAMP_DIFF(CURRENT_TIMESTAMP(), replication_time, SECOND) AS replication_lag_seconds, -- RLS
 -- Calculate the replication lag in minutes.
 TIMESTAMP_DIFF(CURRENT_TIMESTAMP(), replication_time, MINUTE) AS replication_lag_minutes, -- RLM
 -- Show the last sync time for easier interpretation.
 replication_time AS secondary_replica_fully_synced_as_of_time,
FROM
 `region-us`.INFORMATION_SCHEMA.SCHEMATA_REPLICAS
```

The result is similar to the following:

``` text
+---------------------+-------------+--------------+-----+-----+-------------------------------------------+
|    catalog_name     | schema_name | replica_name | rls | rlm | secondary_replica_fully_synced_as_of_time |
+---------------------+-------------+--------------+-----+-----+-------------------------------------------+
| myproject           | my_schema1  | us-east4     |  23 |   0 |                       2023-06-15 00:18:49 |
| myproject           | my_schema2  | us           |  67 |   1 |                       2023-06-15 00:22:49 |
| myproject           | my_schema1  | my_replica   |  11 |   0 |                       2023-06-15 00:28:49 |
| myproject           | my_schema2  | my_replica2  | 125 |   2 |                       2023-06-15 00:29:20 |
+---------------------+-------------+--------------+-----+-----+-------------------------------------------+
```

A value of `  NULL  ` indicates that the secondary replica was never fully synced to the primary replica.
