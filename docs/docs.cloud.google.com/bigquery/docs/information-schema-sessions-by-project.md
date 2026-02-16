# SESSIONS\_BY\_PROJECT view

The `  INFORMATION_SCHEMA.SESSIONS_BY_PROJECT  ` view contains real-time metadata about all BigQuery sessions in the current project.

**Note:** The view names `  INFORMATION_SCHEMA.SESSIONS  ` and `  INFORMATION_SCHEMA.SESSIONS_BY_PROJECT  ` are synonymous and can be used interchangeably.

## Required permissions

To query the `  INFORMATION_SCHEMA.SESSIONS_BY_PROJECT  ` view, you need the `  bigquery.jobs.listAll  ` Identity and Access Management (IAM) permission for the project. Each of the following predefined IAM roles includes the required permission:

  - Project Owner
  - BigQuery Admin

For more information about BigQuery permissions, see [Access control with IAM](/bigquery/docs/access-control) .

## Schema

When you query the `  INFORMATION_SCHEMA.SESSIONS_BY_*  ` views, the query results contain one row for each BigQuery session.

The `  INFORMATION_SCHEMA.SESSIONS_BY_*  ` view has the following schema:

**Note:** The underlying data is partitioned by the `  creation_time  ` column and clustered by `  project_id  ` and `  user_email  ` .

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
<td><code dir="ltr" translate="no">       creation_time      </code></td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td>( <em>Partitioning column</em> ) Creation time of this session. Partitioning is based on the UTC time of this timestamp.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       expiration_time      </code></td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td>( <em>Partitioning column</em> ) Expiration time of this session. Partitioning is based on the UTC time of this timestamp.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       is_active      </code></td>
<td><code dir="ltr" translate="no">       BOOL      </code></td>
<td>Is the session is still active? <code dir="ltr" translate="no">       TRUE      </code> if yes, otherwise <code dir="ltr" translate="no">       FALSE      </code> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       last_modified_time      </code></td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td>( <em>Partitioning column</em> ) Time when the session was last modified. Partitioning is based on the UTC time of this timestamp.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       project_id      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>( <em>Clustering column</em> ) ID of the project.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       project_number      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td>Number of the project.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       session_id      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>ID of the session. For example, <code dir="ltr" translate="no">       bquxsession_1234      </code> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       user_email      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>( <em>Clustering column</em> ) Email address or service account of the user who ran the session.</td>
</tr>
</tbody>
</table>

For stability, we recommend that you explicitly list columns in your information schema queries instead of using a wildcard ( `  SELECT *  ` ). Explicitly listing columns prevents queries from breaking if the underlying schema changes.

## Data retention

This view contains currently running sessions and the history of sessions completed in the past 180 days.

## Scope and syntax

Queries against this view must include a [region qualifier](/bigquery/docs/information-schema-intro#syntax) . If you do not specify a regional qualifier, metadata is retrieved from all regions. The following table explains the region scope for this view:

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
<td><code dir="ltr" translate="no">       [               PROJECT_ID              .]`region-               REGION              `.INFORMATION_SCHEMA.SESSIONS_BY_PROJECT      </code></td>
<td>Project level</td>
<td><code dir="ltr" translate="no">         REGION       </code></td>
</tr>
</tbody>
</table>

Replace the following:

  - Optional: `  PROJECT_ID  ` : the ID of your Google Cloud project. If not specified, the default project is used.
  - `  REGION  ` : any [dataset region name](/bigquery/docs/locations) . For example, ``  `region-us`  `` .
    **Note:** You must use [a region qualifier](/bigquery/docs/information-schema-intro#region_qualifier) to query `  INFORMATION_SCHEMA  ` views. The location of the query execution must match the region of the `  INFORMATION_SCHEMA  ` view.

## Example

To run the query against a project other than your default project, add the project ID in the following format:

``` text
`PROJECT_ID`.`region-REGION_NAME`.INFORMATION_SCHEMA.SESSIONS_BY_PROJECT
```

For example, ``  `myproject`.`region-us`.INFORMATION_SCHEMA.SESSIONS_BY_PROJECT  `` . The following example lists all users or service accounts that created sessions for a given project within the last day:

``` text
SELECT
  DISTINCT(user_email) AS user
FROM
  `region-us`.INFORMATION_SCHEMA.SESSIONS_BY_PROJECT
WHERE
  is_active = true
  AND creation_time >= TIMESTAMP_SUB(CURRENT_TIMESTAMP(), INTERVAL 1 DAY);
```

**Note:** `  INFORMATION_SCHEMA  ` view names are case-sensitive.

The result is similar to the following:

``` text
+--------------+
| user         |
+--------------+
| abc@xyz.com  |
+--------------+
| def@xyz.com  |
+--------------+
```
