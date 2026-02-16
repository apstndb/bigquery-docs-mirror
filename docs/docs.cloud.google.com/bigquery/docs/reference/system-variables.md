# System variables reference

BigQuery supports the following system variables for [multi-statement queries](/bigquery/docs/multi-statement-queries) or within [sessions](/bigquery/docs/sessions-intro) . You can use system variables to set or retrieve information during query execution, similar to user-defined [procedural language variables](/bigquery/docs/multi-statement-queries#variables) .

<table>
<thead>
<tr class="header">
<th>Name</th>
<th>Type</th>
<th>Read and write or read-only</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       @@current_job_id      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Read-only</td>
<td>Job ID of the currently executing job. In the context of a multi-statement query, this returns the job responsible for the current statement, not the entire multi-statement query.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       @@dataset_id      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Read and write</td>
<td>ID of the default dataset in the current project. This ID is used when a dataset is not specified for a project in the query. You can use the <code dir="ltr" translate="no">       SET      </code> statement to assign <code dir="ltr" translate="no">       @@dataset_id      </code> to another dataset ID in the current project. The system variables <code dir="ltr" translate="no">       @@dataset_project_id      </code> and <code dir="ltr" translate="no">       @@dataset_id      </code> can be set and used together.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       @@dataset_project_id      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Read and write</td>
<td>ID of the default project that's used when one is not specified for a dataset used in the query. If <code dir="ltr" translate="no">       @@dataset_project_id      </code> is not set, or if it is set to <code dir="ltr" translate="no">       NULL      </code> , the query-executing project ( <code dir="ltr" translate="no">       @@project_id      </code> ) is used. You can use the <code dir="ltr" translate="no">       SET      </code> statement to assign <code dir="ltr" translate="no">       @@dataset_project_id      </code> to another project ID. The system variables <code dir="ltr" translate="no">       @@dataset_project_id      </code> and <code dir="ltr" translate="no">       @@dataset_id      </code> can be set and used together.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       @@last_job_id      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Read-only</td>
<td>Job ID of the most recent job to execute in the current multi-statement query, not including the current one. If the multi-statement query contains <code dir="ltr" translate="no">       CALL      </code> statements, this job may have originated in a different procedure.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       @@location      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Read and write</td>
<td>The location in which to run the query. <code dir="ltr" translate="no">       @@location      </code> can only be set to a string literal with a <a href="/bigquery/docs/locations#supported_locations">valid location</a> . A <code dir="ltr" translate="no">       SET @@location      </code> statement must be the first statement in a query. An error occurs if there is a mismatch between <code dir="ltr" translate="no">       @@location      </code> and another <a href="/bigquery/docs/locations#specify_locations">location setting</a> for the query. You can improve the latency of queries that set <code dir="ltr" translate="no">       @@location      </code> by using <a href="/bigquery/docs/running-queries#optional-job-creation">optional job creation mode</a> . You can use the <code dir="ltr" translate="no">       @@location      </code> system variable inside of <a href="/bigquery/docs/user-defined-functions#sql-udf-structure">SQL UDFs</a> and <a href="/bigquery/docs/table-functions">table functions</a> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       @@project_id      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Read-only</td>
<td>ID of the project used to execute the current query. In the context of a procedure, <code dir="ltr" translate="no">       @@project_id      </code> refers to the project that is running the multi-statement query, not the project which owns the procedure.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       @@query_label      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Read and write</td>
<td>Query label to associate with query jobs in the current multi-statement query or session. If set in a query, all subsequent query jobs in the script or session will have this label. If not set in a query, the value for this system variable is <code dir="ltr" translate="no">       NULL      </code> . For an example of how to set this system variable, see <a href="/bigquery/docs/adding-labels#adding-label-to-session">Associate jobs in a session with a label</a> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       @@reservation      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Read and write</td>
<td>[ <a href="https://cloud.google.com/products#product-launch-stages">Preview</a> ]. Specifies the reservation where the job is run. Must be in the following format: <code dir="ltr" translate="no">       projects/               project_id              /locations/               location              /reservations/               reservation_id       </code> . The location of the reservation must match the location the query is running in.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       @@row_count      </code></td>
<td><code dir="ltr" translate="no">       INT64      </code></td>
<td>Read-only</td>
<td>If used in a multi-statement query and the previous statement is DML, specifies the number of rows inserted, modified, or deleted, as a result of that DML statement. If the previous statement is a `MERGE` statement, <code dir="ltr" translate="no">       @@row_count      </code> represents the combined total number of rows inserted, modified, and deleted. This value is <code dir="ltr" translate="no">       NULL      </code> if not in a multi-statement query.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       @@script.bytes_billed      </code></td>
<td><code dir="ltr" translate="no">       INT64      </code></td>
<td>Read-only</td>
<td>Total bytes billed so far in the currently executing multi-statement query job. This value is <code dir="ltr" translate="no">       NULL      </code> if not in the job.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       @@script.bytes_processed      </code></td>
<td><code dir="ltr" translate="no">       INT64      </code></td>
<td>Read-only</td>
<td>Total bytes processed so far in the currently executing multi-statement query job. This value is <code dir="ltr" translate="no">       NULL      </code> if not in the job.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       @@script.creation_time      </code></td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td>Read-only</td>
<td>Creation time of the currently executing multi-statement query job. This value is <code dir="ltr" translate="no">       NULL      </code> if not in the job.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       @@script.job_id      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Read-only</td>
<td>Job ID of the currently executing multi-statement query job. This value is <code dir="ltr" translate="no">       NULL      </code> if not in the job.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       @@script.num_child_jobs      </code></td>
<td><code dir="ltr" translate="no">       INT64      </code></td>
<td>Read-only</td>
<td>Number of currently completed child jobs. This value is <code dir="ltr" translate="no">       NULL      </code> if not in the job.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       @@script.slot_ms      </code></td>
<td><code dir="ltr" translate="no">       INT64      </code></td>
<td>Read-only</td>
<td>Number of slot milliseconds used so far by the script. This value is <code dir="ltr" translate="no">       NULL      </code> if not in the job.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       @@session_id      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Read-only</td>
<td>ID of the session that the current query is associated with.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       @@time_zone      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Read and write</td>
<td>The default time zone to use in time zone-dependent SQL functions, when a time zone is not specified as an argument. <code dir="ltr" translate="no">       @@time_zone      </code> can be modified by using a <code dir="ltr" translate="no">       SET      </code> statement to any valid time zone name. At the start of each script, <code dir="ltr" translate="no">       @@time_zone      </code> begins as “UTC”.</td>
</tr>
</tbody>
</table>

For backward compatibility, expressions used in an `  OPTIONS  ` or `  FOR SYSTEM TIME AS OF  ` clause default to the `  America/Los_Angeles  ` time zone, while all other date/time expressions default to the `  UTC  ` time zone. If `  @@time_zone  ` has been set earlier in the multi-statement query, the chosen time zone will apply to all date/time expressions, including `  OPTIONS  ` and `  FOR SYSTEM TIME AS OF  ` clauses.

In addition to the system variables shown previously, you can use `  EXCEPTION  ` system variables during execution of a multi-statement query. For more information about the `  EXCEPTION  ` system variables, see the procedural language statement [BEGIN...EXCEPTION](/bigquery/docs/reference/standard-sql/procedural-language#beginexceptionend) .

## Examples

You don't create system variables, but you can override the default value for some of them:

``` text
SET @@dataset_project_id = 'MyProject';
```

The following query returns the default time zone:

``` text
SELECT @@time_zone AS default_time_zone;
```

``` text
+-------------------+
| default_time_zone |
+-------------------+
| UTC               |
+-------------------+
```

You can use system variables with DDL and DML queries. For example, here are a few ways to use the system variable `  @@time_zone  ` when creating and updating a table:

``` text
BEGIN
  CREATE TEMP TABLE MyTempTable
  AS SELECT @@time_zone AS default_time_zone;
END;
```

``` text
CREATE OR REPLACE TABLE MyDataset.MyTable(default_time_zone STRING)
  OPTIONS (description = @@time_zone);
```

``` text
UPDATE MyDataset.MyTable
SET default_time_zone = @@time_zone
WHERE TRUE;
```

There are some places where system variables can't be used in DDL and DML queries. For example, you can't use a system variable as a project name, dataset, or table name. The following query produces an error when you include the `  @@dataset_id  ` system variable in a table path:

``` text
BEGIN
  CREATE TEMP TABLE @@dataset_id.MyTempTable (id STRING);
END;
```

For more examples of how you can use system variables in multi-statement queries, see [Set a variable](/bigquery/docs/multi-statement-queries#set_system_variable) .

For examples of how you can use system variables in sessions, see [Example session](/bigquery/docs/sessions-write-queries#session_system_variables) .
