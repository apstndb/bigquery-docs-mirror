# EFFECTIVE\_PROJECT\_OPTIONS view

You can query the `  INFORMATION_SCHEMA.EFFECTIVE_PROJECT_OPTIONS  ` view to retrieve real-time metadata about BigQuery effective project options. This view contains configuration options that are set at the organization or project level. If the same configuration option is set at both the organization and project level, the project configuration value is shown. To view the default values for a configuration option, see [configuration settings](/bigquery/docs/default-configuration#configuration-settings) .

## Required permissions

To get effective project options metadata, you need the `  bigquery.config.get  ` Identity and Access Management (IAM) permission.

The following predefined IAM role includes the permissions that you need in order to get effective project options metadata:

  - `  roles/bigquery.jobUser  `

For more information about granular BigQuery permissions, see [roles and permissions](/bigquery/docs/access-control) .

## Schema

When you query the `  INFORMATION_SCHEMA.EFFECTIVE_PROJECT_OPTIONS  ` view, the query results contain one row for each configuration in a project.

The `  INFORMATION_SCHEMA.EFFECTIVE_PROJECT_OPTIONS  ` view has the following schema:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Column name</th>
<th>Data type</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       project_id      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The ID of the project.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       project_number      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td>Number of the project.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         option_name       </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Option ID for the specified configuration setting.</td>
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
<td><code dir="ltr" translate="no">       option_set_level      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The level in the hierarchy at which the setting is defined, with possible values of <code dir="ltr" translate="no">       DEFAULT      </code> , <code dir="ltr" translate="no">       ORGANIZATION      </code> , or <code dir="ltr" translate="no">       PROJECTS      </code> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       option_set_on_id      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Set value based on value of <code dir="ltr" translate="no">       option_set_level      </code> :
<ul>
<li>If <code dir="ltr" translate="no">         DEFAULT        </code> , set to <code dir="ltr" translate="no">         null        </code> .</li>
<li>If <code dir="ltr" translate="no">         ORGANIZATION        </code> , set to <code dir="ltr" translate="no">         ""        </code> .</li>
<li>If <code dir="ltr" translate="no">         PROJECT        </code> , set to <code dir="ltr" translate="no">         ID        </code> .</li>
</ul></td>
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
<td>The effective default time zone for this project.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       default_kms_key_name      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The effective default key name for this project.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       default_query_job_timeout_ms      </code></td>
<td><code dir="ltr" translate="no">       INT64      </code></td>
<td>The effective default query timeout in milliseconds for this project.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       default_interactive_query_queue_timeout_ms      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The effective default timeout in milliseconds for queued interactive queries for this project.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       default_batch_query_queue_timeout_ms      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The effective default timeout in milliseconds for queued batch queries for this project.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       enable_reservation_based_fairness      </code></td>
<td><code dir="ltr" translate="no">       BOOL      </code></td>
<td>Use reservation-based fairness as opposed to project-based fairness.</td>
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
<td><code dir="ltr" translate="no">       `region-               REGION              `.INFORMATION_SCHEMA.EFFECTIVE_PROJECT_OPTIONS      </code></td>
<td>Configuration options within the specified project.</td>
<td><code dir="ltr" translate="no">         REGION       </code></td>
</tr>
</tbody>
</table>

Replace the following:

  - `  REGION  ` : any [dataset region name](/bigquery/docs/locations) . For example, `  region-us  ` .

## Examples

The following example retrieves the `  OPTION_NAME  ` , `  OPTION_TYPE  ` , `  OPTION_VALUE  ` , `  OPTION_SET_LEVEL  ` , and `  OPTION_SET_ON_ID  ` columns from the `  INFORMATION_SCHEMA.EFFECTIVE_PROJECT_OPTIONS  ` view.

``` text
SELECT
  option_name, option_type, option_value, option_set_level, option_set_on_id
FROM
  `region-REGION`.INFORMATION_SCHEMA.EFFECTIVE_PROJECT_OPTIONS;
```

**Note:** `  INFORMATION_SCHEMA  ` view names are case-sensitive.

The result is similar to the following:

``` text
  +--------------------------------------------+-------------+---------------------+------------------+--------------------+
  | option_name                                | option_type | option_value        | option_set_level | option_set_on_id   |
  +--------------------------------------------+-------------+---------------------+------------------+--------------------+
  | default_time_zone                          | STRING      | America/Los_Angeles | organizations    | my_organization_id |
  +--------------------------------------------+-------------+---------------------+------------------+--------------------+
  | default_kms_key_name                       | STRING      | test/testkey1       | projects         | my_project_id      |
  +--------------------------------------------+-------------+---------------------+------------------+--------------------+
  | default_query_job_timeout_ms               | INT64       | 18000000            | projects         | my_project_id      |
  +--------------------------------------------+-------------+---------------------+------------------+--------------------+
  | default_interactive_query_queue_timeout_ms | INT64       | 600000              | organization     | my_organization_id |
  +--------------------------------------------+-------------+---------------------+------------------+--------------------+
  | default_batch_query_queue_timeout_ms       | INT64       | 1200000             | projects         | my_project_id      |
  +--------------------------------------------+-------------+---------------------+------------------+--------------------+
  
```
