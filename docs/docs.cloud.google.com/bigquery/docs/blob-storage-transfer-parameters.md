# Runtime parameters in Blob Storage transfers

When you set up a data transfer in Cloud Storage, Azure Blob Storage, or Amazon Simple Storage Service (Amazon S3), you can parameterize the URI (or data path) and the destination table. Parameterizing lets you load data from buckets that are organized by date. These parameters are referred to as *runtime parameters* to distinguish them from query parameters.

When you use runtime parameters in a transfer, you can do the following:

  - Specify how you want to partition the destination table
  - Retrieve files that match a particular date

## Available runtime parameters

When you set up the Cloud Storage, Blob Storage, or Amazon S3 transfer, you can specify how you want to partition the destination table by using runtime parameters.

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Parameter</strong></th>
<th><strong>Template type</strong></th>
<th><strong>Value</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       run_time      </code></td>
<td>Formatted timestamp</td>
<td>In UTC time, per the schedule. For regularly scheduled transfers, <code dir="ltr" translate="no">       run_time      </code> represents the intended time of execution. For example, if the transfer is set to "every 24 hours", the <code dir="ltr" translate="no">       run_time      </code> difference between two consecutive queries will be exactly 24 hours—even though the actual execution time might vary slightly.<br />
<br />
See <a href="/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs.runs">TransferRun.runTime</a></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       run_date      </code></td>
<td>Date string</td>
<td>The date of the <code dir="ltr" translate="no">       run_time      </code> parameter in the following format: <code dir="ltr" translate="no">       %Y%m%d      </code> ; for example, <em>20180101</em> . This format is compatible with ingestion-time partitioned tables.</td>
</tr>
</tbody>
</table>

## Templating system

Cloud Storage, Blob Storage, and Amazon S3 transfers support runtime parameters in the destination table name by using a templating syntax.

#### Parameter templating syntax

The templating syntax supports basic string templating and time offsetting. Parameters are referenced in the following formats:

  - `  {run_date}  `
  - `  {run_time[+\-offset]|"time_format"}  `

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Parameter</strong></th>
<th><strong>Purpose</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       run_date      </code></td>
<td>This parameter is replaced by the date in format <code dir="ltr" translate="no">       YYYYMMDD      </code> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       run_time      </code></td>
<td>This parameter supports the following properties:
<p><br />
<code dir="ltr" translate="no">        offset       </code><br />
Time offset expressed in hours (h), minutes (m), and seconds (s) in that order.<br />
Days (d) are not supported.<br />
Decimals are allowed, for example: <code dir="ltr" translate="no">        1.5h       </code> .</p>
<p><code dir="ltr" translate="no">        time_format       </code><br />
A formatting string. The most common formatting parameters are years (%Y), months (%m), and days (%d).<br />
For partitioned tables, YYYYMMDD is the required suffix - this is equivalent to "%Y%m%d".<br />
<br />
Read more about <a href="/bigquery/docs/reference/standard-sql/functions-and-operators#supported-format-elements-for-datetime">formatting datetime elements</a> .</p></td>
</tr>
</tbody>
</table>

**Usage notes:**

  - No whitespace is allowed between run\_time, offset, and time format.
  - To include literal curly braces in the string, you can escape them as `  '\{' and '\}'  ` .
  - To include literal quotes or a vertical bar in the time\_format, such as `  "YYYY|MM|DD"  ` , you can escape them in the format string as: `  '\"'  ` or `  '\|'  ` .

#### Parameter templating examples

These examples demonstrate specifying destination table names with different time formats, and offsetting the run time.

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>run_time (UTC)</strong></th>
<th><strong>Templated parameter</strong></th>
<th><strong>Output destination table name</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>2018-02-15 00:00:00</td>
<td><code dir="ltr" translate="no">       mytable      </code></td>
<td><code dir="ltr" translate="no">       mytable      </code></td>
</tr>
<tr class="even">
<td>2018-02-15 00:00:00</td>
<td><code dir="ltr" translate="no">       mytable_{               run_time|"%Y%m%d"              }      </code></td>
<td><code dir="ltr" translate="no">       mytable_20180215      </code></td>
</tr>
<tr class="odd">
<td>2018-02-15 00:00:00</td>
<td><code dir="ltr" translate="no">       mytable_{               run_time+25h|"%Y%m%d"              }      </code></td>
<td><code dir="ltr" translate="no">       mytable_20180216      </code></td>
</tr>
<tr class="even">
<td>2018-02-15 00:00:00</td>
<td><code dir="ltr" translate="no">       mytable_{               run_time-1h|"%Y%m%d"              }      </code></td>
<td><code dir="ltr" translate="no">       mytable_20180214      </code></td>
</tr>
<tr class="odd">
<td>2018-02-15 00:00:00</td>
<td><code dir="ltr" translate="no">       mytable_{               run_time+1.5h|"%Y%m%d%H"              }      </code><br />
or<br />
<code dir="ltr" translate="no">       mytable_{               run_time+90m|"%Y%m%d%H"              }      </code></td>
<td><code dir="ltr" translate="no">       mytable_2018021501      </code></td>
</tr>
<tr class="even">
<td>2018-02-15 00:00:00</td>
<td><code dir="ltr" translate="no">       {               run_time+97s|"%Y%m%d"              }_mytable_{               run_time+97s|"%H%M%S"              }      </code></td>
<td><code dir="ltr" translate="no">       20180215_mytable_000137      </code></td>
</tr>
</tbody>
</table>

**Note:** When you use date or time parameters to create tables with names ending in a date format such as `  YYYYMMDD  ` , BigQuery [groups these tables together](/bigquery/docs/querying-wildcard-tables) . In the Google Cloud console, these grouped tables might be displayed with a name like `  mytable_(1)  ` , which represents the collection of sharded tables.

## Partitioning options

There are two types of partitioned tables in BigQuery:

  - **Tables that are partitioned by ingestion time.** For Cloud Storage, Blob Storage, and Amazon S3 transfers, the ingestion time is the transfer's run time.
  - **Tables that are partitioned based on a column.** The column type must be a [`  TIMESTAMP  `](/bigquery/docs/reference/standard-sql/data-types#timestamp_type) or [`  DATE  `](/bigquery/docs/reference/standard-sql/data-types#date_type) column.

If the destination table is partitioned on a column, you identify the partitioning column when you create the destination table and specify its schema. Learn more about creating column-based partitioned tables in [Creating and using partitioned tables](/bigquery/docs/creating-column-partitions) .

**Note:** Minutes cannot be specified when partitioning a table.

### Partitioning examples

  - Table with no partitioning
      - Destination table: `  mytable  `
  - [Ingestion-time partitioned table](/bigquery/docs/partitioned-tables#ingestion_time)
      - Destination table: `  mytable $YYYYMMDD  `
      - Note that minutes cannot be specified.
  - [Column-partitioned table](/bigquery/docs/partitioned-tables#date_timestamp_partitioned_tables)
      - Destination table: `  mytable  `
      - Specify the partitioning column as a `  TIMESTAMP  ` or `  DATE  ` column when you create the table's schema.

## Notes on parameter usage

  - If you partition your data based on your local timezone, you need to manually calculate the hour offset from UTC by using the offsetting mechanism in the [templating syntax](#templating_system) .
  - Minutes cannot be specified in parameters.
  - Using wildcards for the URI or data path in combination with parameters on the destination table name is allowed.

## Runtime parameter examples

The following examples show ways to combine the wildcard character and parameters for common use cases. Assume the table's name is `  mytable  ` and the `  run_time  ` is `  2018-02-15 00:00:00  ` (UTC) for all examples.

### Transfer data to a non-partitioned table

This use case applies to loading new files from a Cloud Storage, Blob Storage, or Amazon S3 bucket into a non-partitioned table. This example uses a wildcard in the URI or data path and uses an ad hoc refresh transfer to pick up new files.

<table>
<thead>
<tr class="header">
<th><strong>Data source</strong></th>
<th><strong>Source URI or data path</strong></th>
<th><strong>Destination table name</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Cloud Storage</td>
<td><code dir="ltr" translate="no">       gs://bucket/*.csv      </code></td>
<td><code dir="ltr" translate="no">       mytable      </code></td>
</tr>
<tr class="even">
<td>Amazon S3</td>
<td><code dir="ltr" translate="no">       s3://bucket/*.csv      </code></td>
<td><code dir="ltr" translate="no">       mytable      </code></td>
</tr>
<tr class="odd">
<td>Blob Storage</td>
<td><code dir="ltr" translate="no">       *.csv      </code></td>
<td><code dir="ltr" translate="no">       mytable      </code></td>
</tr>
</tbody>
</table>

### Load a snapshot of all data into an ingestion-time partitioned table

In this case, all data in the specified URI or data path is transferred to a table partitioned by today's date. In a refresh transfer, this configuration picks up files added since the last load and adds them to a particular partition.

<table>
<thead>
<tr class="header">
<th><strong>Data source</strong></th>
<th><strong>Source URI or data path</strong></th>
<th><strong>Parameterized destination table name</strong></th>
<th><strong>Evaluated destination table name</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Cloud Storage</td>
<td><code dir="ltr" translate="no">       gs://bucket/*.csv      </code></td>
<td><code dir="ltr" translate="no">       mytable${               run_time|"%Y%m%d"              }      </code></td>
<td><code dir="ltr" translate="no">       mytable$20180215      </code></td>
</tr>
<tr class="even">
<td>Amazon S3</td>
<td><code dir="ltr" translate="no">       s3://bucket/*.csv      </code></td>
<td><code dir="ltr" translate="no">       mytable${               run_time|"%Y%m%d"              }      </code></td>
<td><code dir="ltr" translate="no">       mytable$20180215      </code></td>
</tr>
<tr class="odd">
<td>Blob Storage</td>
<td><code dir="ltr" translate="no">       *.csv      </code></td>
<td><code dir="ltr" translate="no">       mytable${               run_time|"%Y%m%d"              }      </code></td>
<td><code dir="ltr" translate="no">       mytable$20180215      </code></td>
</tr>
</tbody>
</table>

This use case transfers today's data into a table partitioned on today's date. This example also applies to a refresh transfer that retrieves newly added files that match a certain date and loads the data into the corresponding partition.

<table>
<thead>
<tr class="header">
<th><strong>Data source</strong></th>
<th><strong>Parameterized URI or data path</strong></th>
<th><strong>Parameterized destination table name</strong></th>
<th><strong>Evaluated URI or data path</strong></th>
<th><strong>Evaluated destination table name</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Cloud Storage</td>
<td><code dir="ltr" translate="no">       gs://bucket/events-{               run_time|"%Y%m%d"              }/*.csv      </code></td>
<td><code dir="ltr" translate="no">       mytable${               run_time|"%Y%m%d"              }      </code></td>
<td><code dir="ltr" translate="no">       gs://bucket/events-20180215/*.csv      </code></td>
<td><code dir="ltr" translate="no">       mytable$20180215      </code></td>
</tr>
<tr class="even">
<td>Amazon S3</td>
<td><code dir="ltr" translate="no">       s3://bucket/events-{               run_time|"%Y%m%d"              }/*.csv      </code></td>
<td><code dir="ltr" translate="no">       mytable${               run_time|"%Y%m%d"              }      </code></td>
<td><code dir="ltr" translate="no">       s3://bucket/events-20180215/*.csv      </code></td>
<td><code dir="ltr" translate="no">       mytable$20180215      </code></td>
</tr>
<tr class="odd">
<td>Blob Storage</td>
<td><code dir="ltr" translate="no">       events-{               run_time|"%Y%m%d"              }/*.csv      </code></td>
<td><code dir="ltr" translate="no">       mytable${               run_time|"%Y%m%d"              }      </code></td>
<td><code dir="ltr" translate="no">       events-20180215/*.csv      </code></td>
<td><code dir="ltr" translate="no">       mytable$20180215      </code></td>
</tr>
</tbody>
</table>

## What's next

  - Learn more about [setting up an Azure Blob Storage transfer](/bigquery/docs/blob-storage-transfer) .
  - Learn more about the [BigQuery Data Transfer Service](/bigquery/docs/dts-introduction) .
