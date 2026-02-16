# System procedures reference

BigQuery supports the following system procedures, which can be used similarly to user-created [stored procedures](/bigquery/docs/procedures) .

## BQ.ABORT\_SESSION

**Syntax**

``` text
CALL BQ.ABORT_SESSION([session_id]);
```

**Description**

Terminates your current session.

You can optionally specify the [session ID](/bigquery/docs/sessions#get-id) , which lets you terminate a session if the system procedure isn't called from that session.

For more information, see [Terminating sessions](/bigquery/docs/sessions#terminate-session) .

## BQ.JOBS.CANCEL

**Syntax**

``` text
CALL BQ.JOBS.CANCEL(job);
```

**Description**

Cancels a running job.

Specify the job as a string with the format `  '[project_id.]job_id'  ` . If you run this system procedure from a different project than the job, then you must include the project ID. You must run the procedure in the same location as the job.

For more information, see [Canceling a job](/bigquery/docs/managing-jobs#cancel_jobs) .

## BQ.CANCEL\_INDEX\_ALTERATION

**Syntax**

``` text
CALL BQ.CANCEL_INDEX_ALTERATION(table_name, index_name);
```

**Description**

Cancels a user-initiated [rebuild of a vector index](/bigquery/docs/reference/standard-sql/data-definition-language#alter_vector_index_rebuild_statement) .

Specify the name of the table as a string with the format `  '[project_id.]dataset.table'  ` and the index name as a string. If you run this system procedure from a different project than the table, then you must include the project ID.

You must run this procedure in the same location as the indexed table. To set the location of your query, see [Specify locations](/bigquery/docs/locations#specify_locations) .

**Example**

``` text
CALL BQ.CANCEL_INDEX_ALTERATION('my_project.my_dataset.indexed_table', 'my_index');
```

## BQ.REFRESH\_EXTERNAL\_METADATA\_CACHE

**Syntax**

``` text
CALL BQ.REFRESH_EXTERNAL_METADATA_CACHE(table_name [, [subdirectory_uri, …]]);
```

**Description**

Refreshes the metadata cache of a BigLake table or an object table. This procedure fails if you run it against a table that has the metadata caching mode set to `  AUTOMATIC  ` .

To run this system procedure, you need the `  bigquery.tables.update  ` and `  bigquery.tables.updateData  ` permissions.

Specify the name of the table as a string with the format `  '[project_id.]dataset.table'  ` . If you run this system procedure from a different project than the table, then you must include the project ID.

For BigLake tables, you can optionally specify one or more subdirectories of the table data directory in Cloud Storage in the format `  'gs://table_data_directory/subdirectory/.../'  ` . This lets you refresh only the table metadata from those subdirectories and thereby avoid unnecessary metadata processing.

**Examples**

To refresh all of the metadata for a table:

``` text
CALL BQ.REFRESH_EXTERNAL_METADATA_CACHE('myproject.test_db.test_table')
```

To selectively refresh the metadata for a BigLake table:

``` text
CALL BQ.REFRESH_EXTERNAL_METADATA_CACHE('myproject.test_db.test_table', ['gs://source/uri/sub/path/d1/*', 'gs://source/uri/sub/path/d2/*'])
```

**Limitation**

  - Metadata cache refresh is not supported for tables referenced by linked datasets over external datasets.
  - Metadata cache refresh shouldn't be used in a [Multi-statement transaction](/bigquery/docs/transactions) .

## BQ.REFRESH\_MATERIALIZED\_VIEW

**Syntax**

``` text
CALL BQ.REFRESH_MATERIALIZED_VIEW(view_name);
```

**Description**

Refreshes a materialized view.

Specify the name of the materialized view as a string with the format `  '[project_id.]dataset.table'  ` . If you run this system procedure from a different project than the materialized view, then you must include the project ID.

For more information, see [Manual refresh](/bigquery/docs/materialized-views#manual_refresh) .
