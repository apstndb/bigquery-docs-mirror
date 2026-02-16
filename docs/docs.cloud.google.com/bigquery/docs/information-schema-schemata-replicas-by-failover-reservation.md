# SCHEMATA\_REPLICAS\_BY\_FAILOVER\_RESERVATION view

The `  INFORMATION_SCHEMA.SCHEMATA_REPLICAS_BY_FAILOVER_RESERVATION  ` view contains information about schemata replicas associated with a failover reservation. The `  INFORMATION_SCHEMA.SCHEMATA_REPLICAS_BY_FAILOVER_RESERVATION  ` view is scoped to the project of the failover reservation, as opposed to the [`  INFORMATION_SCHEMA.SCHEMATA_REPLICAS  ` view](/bigquery/docs/information-schema-schemata-replicas) that is scoped to the project that contains the dataset.

## Required role

To get the permissions that you need to query the `  INFORMATION_SCHEMA.SCHEMATA_REPLICAS_BY_FAILOVER_RESERVATION  ` view, ask your administrator to grant you the [BigQuery Resource Viewer](/iam/docs/roles-permissions/bigquery#bigquery.resourceViewer) ( `  roles/bigquery.resourceViewer  ` ) IAM role on the project. For more information about granting roles, see [Manage access to projects, folders, and organizations](/iam/docs/granting-changing-revoking-access) .

You might also be able to get the required permissions through [custom roles](/iam/docs/creating-custom-roles) or other [predefined roles](/iam/docs/roles-overview#predefined) .

## Schema

The `  INFORMATION_SCHEMA.SCHEMATA_REPLICAS_BY_FAILOVER_RESERVATION  ` view has the following schema:

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
<td><code dir="ltr" translate="no">       failover_reservation_project_id      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The project ID of the failover reservation admin project if it's associated with the replica.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       failover_reservation_name      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The name of the failover reservation if it's associated with the replica.</td>
</tr>
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
<td><code dir="ltr" translate="no">       [               RESERVATION_PROJECT_ID              .]`region-               REGION              `.INFORMATION_SCHEMA.SCHEMATA_REPLICAS_BY_FAILOVER_RESERVATION[_BY_PROJECT]      </code></td>
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

This section lists example queries of the `  INFORMATION_SCHEMA.SCHEMATA_REPLICAS_BY_FAILOVER_RESERVATION  ` view.

**Example: List all replicated datasets in a region**

The following example lists all the replicated datasets in the `  US  ` region:

``` text
SELECT *
FROM `region-us`.INFORMATION_SCHEMA.SCHEMATA_REPLICAS_BY_FAILOVER_RESERVATION
WHERE failover_reservation_name = "failover_reservation";
```

The result is similar to the following:

``` text
+--------------+--------------+--------------+----------+--------------------------+-------------------------------------+---------------------+-------------------+---------------------+---------------------------------+---------------------------+-------------------------------------------------------------------------------+
| catalog_name | schema_name  | replica_name | location | replica_primary_assigned | replica_primary_assignment_complete |    creation_time    | creation_complete |  replication_time   | failover_reservation_project_id | failover_reservation_name |                                  sync_status                                  |
+--------------+--------------+--------------+----------+--------------------------+-------------------------------------+---------------------+-------------------+---------------------+---------------------------------+---------------------------+-------------------------------------------------------------------------------+
| project2     | test_dataset | us-east4     | us-east4 |                     true |                                true | 2024-05-09 20:34:06 |              true |                NULL | project1                        | failover_reservation      |                                                                          NULL |
| project2     | test_dataset | us           | US       |                    false |                               false | 2024-05-09 20:34:05 |              true | 2024-05-10 18:31:06 | project1                        | failover_reservation      | {"last_completion_time":"2024-06-06 18:31:06","error_time":null,"error":null} |
+--------------+--------------+--------------+----------+--------------------------+-------------------------------------+---------------------+-------------------+---------------------+---------------------------------+---------------------------+-------------------------------------------------------------------------------+
```
