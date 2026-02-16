# Introduction to data export

This document describes the different ways of exporting data from BigQuery.

For more information about data integrations, see [Introduction to loading, transforming, and exporting data](/bigquery/docs/load-transform-export-intro) .

## Export query results

You can export query results to a local file (either as a CSV or JSON file), Google Drive, or Google Sheets. For more information, see [Export query results to a file](/bigquery/docs/export-file) .

## Export tables

You can export your BigQuery tables in the following data formats:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Data format</th>
<th>Supported compression types</th>
<th>Supported export methods</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>CSV</td>
<td>GZIP</td>
<td><a href="/bigquery/docs/exporting-data">Export to Cloud Storage</a></td>
</tr>
<tr class="even">
<td>JSON</td>
<td>GZIP</td>
<td><a href="/bigquery/docs/exporting-data">Export to Cloud Storage</a><br />
<a href="/dataflow/docs/guides/read-from-bigquery">Read from BigQuery using Dataflow</a></td>
</tr>
<tr class="odd">
<td>Avro</td>
<td>DEFLATE, SNAPPY</td>
<td><a href="/bigquery/docs/exporting-data">Export to Cloud Storage</a><br />
<a href="/dataflow/docs/guides/read-from-bigquery">Read from BigQuery using Dataflow</a></td>
</tr>
<tr class="even">
<td>Parquet</td>
<td>GZIP, SNAPPY, ZSTD</td>
<td><a href="/bigquery/docs/exporting-data">Export to Cloud Storage</a></td>
</tr>
</tbody>
</table>

You can also [export your BigQuery tables as Protobuf columns](/bigquery/docs/protobuf-export) when working with nested data structures that require object type safety, or if you need a wider language support.

## Export BigQuery code assets

You can download [BigQuery Studio](/bigquery/docs/query-overview#bigquery-studio) code assets, such as [saved queries](/bigquery/docs/saved-queries-introduction) or [notebooks](/bigquery/docs/notebooks-introduction) to maintain a local copy of your assets. For more information on downloading your BigQuery code assets, see the following:

  - [Download saved queries](/bigquery/docs/manage-saved-queries#download_saved_queries)
  - [Download notebooks](/bigquery/docs/manage-notebooks#download_a_notebook)

## Export using reverse ETL

You can set up reverse ETL (RETL) workflows ( [preview](https://cloud.google.com/products#product-launch-stages) ) to move data from BigQuery to the following databases:

  - [Export to Bigtable](/bigquery/docs/export-to-bigtable)
  - [Export to Spanner](/bigquery/docs/export-to-spanner)
  - [Export to Pub/Sub](/bigquery/docs/export-to-pubsub)

## What's next

  - Learn about [quotas for extract jobs](/bigquery/quotas#export_jobs) .
  - Learn about [BigQuery storage pricing](https://cloud.google.com/bigquery/pricing#storage) .
