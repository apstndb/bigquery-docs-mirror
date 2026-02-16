# PROJECT\_OPTIONS\_CHANGES view

You can query the `  INFORMATION_SCHEMA.PROJECT_OPTIONS_CHANGES  ` view to retrieve real-time metadata about BigQuery configuration changes of a project. This view reflects project-level configuration changes made after January 31, 2024.

## Required permissions

To get the configuration, you need the `  bigquery.config.update  ` Identity and Access Management (IAM) permission at the project level. The predefined IAM role `  roles/bigquery.admin  ` includes the permissions that you need to create a configuration.

For more information about granular BigQuery permissions, see [roles and permissions](/bigquery/docs/access-control) .

## Schema

When you query the `  INFORMATION_SCHEMA.PROJECT_OPTIONS_CHANGES  ` view, the query results contain one row for each configuration change in a project.

The `  INFORMATION_SCHEMA.PROJECT_OPTIONS_CHANGES  ` view has the following schema:

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
<td><code dir="ltr" translate="no">       update_time      </code></td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td>The time the configuration change occurred.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       username      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>For first-party users, it's their user email. For third-party users, it's the name that users set in the third-party identity provider.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       updated_options      </code></td>
<td><code dir="ltr" translate="no">       JSON      </code></td>
<td>A JSON object of the configuration options users updated in the change, containing the previous and the new values of updated fields.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       project_id      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The project ID. This field is empty for organization-level configuration changes.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       project_number      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td>The project number. This field is empty for the organization-level configuration changes.</td>
</tr>
</tbody>
</table>

For stability, we recommend that you explicitly list columns in your information schema queries instead of using a wildcard ( `  SELECT *  ` ). Explicitly listing columns prevents queries from breaking if the underlying schema changes.

## Data retention

This view contains sessions that are running and the history of sessions completed in the past 180 days.

## Scope and syntax

Queries against this view must have a [region qualifier](/bigquery/docs/information-schema-intro#syntax) .

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
<td><code dir="ltr" translate="no">       `region-               REGION              `.INFORMATION_SCHEMA.PROJECT_OPTIONS_CHANGES      </code></td>
<td>Configuration changes within the specified project.</td>
<td><code dir="ltr" translate="no">         REGION       </code></td>
</tr>
</tbody>
</table>

Replace the following:

  - `  REGION  ` : any [dataset region name](/bigquery/docs/locations) . For example, `  US  ` , or `  us-west2  ` .

**Note:** To learn how to extract a JSON scalar value from the `  updated_options  ` column and convert it to a SQL STRING value such as `  JSON_VALUE()  ` , see [JSON functions](/bigquery/docs/reference/standard-sql/json_functions#categories) .

## Examples

The following example retrieves all columns from the `  INFORMATION_SCHEMA.PROJECT_OPTIONS_CHANGES  ` view.

``` text
SELECT
  *
FROM
  `region-REGION`.INFORMATION_SCHEMA.PROJECT_OPTIONS_CHANGES;
```

**Note:** `  INFORMATION_SCHEMA  ` view names are case-sensitive.

The result is similar to the following:

``` text
+----------------+------------+-------------------------+-----------------+------------------------------------------------------------------------------------------------------------------+
| project_number | project_id | update_time             | username        | updated_options                                                                                                  |
|----------------|------------|-------------------------|-----------------|------------------------------------------------------------------------------------------------------------------|
| 4471534625     | myproject1 | 2023-08-22 06:57:49 UTC | user1@gmail.com | {"default_query_job_timeout_ms":{"new":0,"old":1860369},"default_time_zone":{"new":"America/New_York","old":""}} |
|----------------|------------|-------------------------|-----------------|------------------------------------------------------------------------------------------------------------------|
| 5027725474     | myproject2 | 2022-08-01 00:00:00 UTC | user2@gmail.com | {"default_interactive_query_queue_timeout_ms":{"new":1860369,"old":1860008}}                                     |
+----------------+------------+-------------------------+-----------------+------------------------------------------------------------------------------------------------------------------+
```
