# PROJECT\_OPTIONS view

You can query the `  INFORMATION_SCHEMA.PROJECT_OPTIONS  ` view to retrieve real-time metadata about BigQuery project options. This view contains configuration options that have been set at the project level. To view the default values for a configuration option, see [configuration settings](/bigquery/docs/default-configuration#configuration-settings) .

## Required permissions

To get configuration options metadata, you need the following Identity and Access Management (IAM) permissions:

  - `  bigquery.config.get  `

The following predefined IAM role includes the permissions that you need in order to get project options metadata:

  - `  roles/bigquery.jobUser  `

For more information about granular BigQuery permissions, see [roles and permissions](/bigquery/docs/access-control) .

## Schema

When you query the `  INFORMATION_SCHEMA.PROJECT_OPTIONS  ` view, the query results contain one row for each configuration option in a project that differs from the default value.

The `  INFORMATION_SCHEMA.PROJECT_OPTIONS  ` view has the following schema:

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
<td><code dir="ltr" translate="no">         option_name       </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Option ID for the specified configuration setting.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       project_id      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The ID of the project.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       project_number      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td>Number of the project.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       option_description      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The option description.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       option_type      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The data type of the <code dir="ltr" translate="no">       OPTION_VALUE      </code> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       option_value      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The current value of the option.</td>
</tr>
</tbody>
</table>

##### Options table

<table>
<thead>
<tr class="header">
<th><code dir="ltr" translate="no">       option_name      </code></th>
<th><code dir="ltr" translate="no">       option_type      </code></th>
<th><code dir="ltr" translate="no">       option_value      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       default_time_zone      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The default time zone for this project.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       default_kms_key_name      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The default key name for this project.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       default_query_job_timeout_ms      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The default query timeout in milliseconds for this project. This also applies to <a href="/bigquery/docs/continuous-queries-introduction">continuous queries</a> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       default_interactive_query_queue_timeout_ms      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The default timeout in milliseconds for queued interactive queries for this project.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       default_batch_query_queue_timeout_ms      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The default timeout in milliseconds for queued batch queries for this project.</td>
</tr>
</tbody>
</table>

For stability, we recommend that you explicitly list columns in your information schema queries instead of using a wildcard ( `  SELECT *  ` ). Explicitly listing columns prevents queries from breaking if the underlying schema changes.

## Data retention

This view contains currently running sessions and the history of sessions completed in the past 180 days.

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
<td><code dir="ltr" translate="no">       `region-               REGION              `.INFORMATION_SCHEMA.PROJECT_OPTIONS      </code></td>
<td>Configuration options within the specified project.</td>
<td><code dir="ltr" translate="no">         REGION       </code></td>
</tr>
</tbody>
</table>

Replace the following:

  - `  REGION  ` : any [dataset region name](/bigquery/docs/locations) . For example, `  region-us  ` .

## Examples

The following example retrieves the `  OPTION_NAME  ` , `  OPTION_TYPE  ` , and `  OPTION_VALUE  ` columns from the `  INFORMATION_SCHEMA.PROJECT_OPTIONS  ` view.

``` text
SELECT
  option_name, option_type, option_value
FROM
  `region-REGION`.INFORMATION_SCHEMA.PROJECT_OPTIONS;
```

**Note:** `  INFORMATION_SCHEMA  ` view names are case-sensitive.

The result is similar to the following:

``` text
  +--------------------------------------------+-------------+---------------------+
  | option_name                                | option_type | option_value        |
  +--------------------------------------------+-------------+---------------------+
  | default_time_zone                          | STRING      | America/Los_Angeles |
  +--------------------------------------------+-------------+---------------------+
  | default_kms_key_name                       | STRING      | test/testkey1       |
  +--------------------------------------------+-------------+---------------------+
  | default_query_job_timeout_ms               | INT64       | 18000000            |
  +--------------------------------------------+-------------+---------------------+
  | default_interactive_query_queue_timeout_ms | INT64       | 600000              |
  +--------------------------------------------+-------------+---------------------+
  | default_batch_query_queue_timeout_ms       | INT64       | 1200000             |
  +--------------------------------------------+-------------+---------------------+
  
```
