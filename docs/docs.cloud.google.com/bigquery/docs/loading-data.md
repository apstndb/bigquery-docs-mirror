# Introduction to loading data

This document explains how you can load data into BigQuery. The two common approaches to data integration are to extract, load, and transform (ELT) or to extract, transform, load (ETL) data.

For an overview of ELT and ETL approaches, see [Introduction to loading, transforming, and exporting data](/bigquery/docs/load-transform-export-intro) .

## Methods of loading or accessing external data

In the BigQuery page, in the [**Add data** dialog](/bigquery/docs/bigquery-web-ui#studio-overview) , you can view all available methods to load data into BigQuery or access data from BigQuery. Choose one of the following options based on your use case and data sources:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Loading method</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>Batch load</strong></td>
<td>This method is suitable for batch loading large volumes of data from a variety of sources.<br />
<br />
For batch or incremental loading of data from Cloud Storage and other supported data sources, we recommend using the <a href="/bigquery/docs/dts-introduction">BigQuery Data Transfer Service</a> .<br />
<br />
With the BigQuery Data Transfer Service, to automate data loading pipelines into BigQuery, you can schedule load jobs. You can schedule one-time or batch data transfers at regular intervals (for example, daily or monthly). To ensure that your BigQuery data is always current, you can monitor and log your transfers.<br />
<br />
For a list of data sources supported by the BigQuery Data Transfer Service, see <a href="/bigquery/docs/dts-introduction#supported_data_sources">Supported data sources</a> .</td>
</tr>
<tr class="even">
<td><strong>Streaming load</strong></td>
<td>This method enables loading data in near real time from messaging systems.<br />
<br />
To stream data into BigQuery, you can use a BigQuery subscription in <a href="/pubsub/docs/overview">Pub/Sub</a> . Pub/Sub can handle high throughput of data loads into BigQuery. It supports real-time data streaming, loading data as it's generated. For more information, see <a href="/pubsub/docs/bigquery">BigQuery subscriptions</a> .</td>
</tr>
<tr class="odd">
<td><strong>Change Data Capture (CDC)</strong></td>
<td>This method enables replicating data from databases to BigQuery in near real time.<br />
<br />
<a href="/datastream/docs/overview">Datastream</a> can stream data from databases to BigQuery data with near real-time replication. Datastream leverages CDC capabilities to track and replicate row-level changes from your data sources.<br />
<br />
For a list of data sources supported by Datastream, see <a href="/datastream/docs/sources">Sources</a> .</td>
</tr>
<tr class="even">
<td><strong>Federation to external data sources</strong></td>
<td>This method enables access to external data without loading it into BigQuery.<br />
<br />
BigQuery supports accessing select <a href="/bigquery/docs/external-data-sources">external data sources</a> through Cloud Storage and federated queries. The advantage of this method is that you don't need to load the data before transforming it for subsequent use. You can perform the transformation by running <code dir="ltr" translate="no">       SELECT      </code> statements over the external data.</td>
</tr>
</tbody>
</table>

You can also use the following programmatic methods to load the data:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Loading method</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>Batch load</strong></td>
<td>You can <a href="/bigquery/docs/batch-loading-data">load data from Cloud Storage or from a local file</a> by creating a load job.<br />
<br />
If your source data changes infrequently, or you don't need continuously updated results, load jobs can be a less expensive, less resource-intensive way to load your data into BigQuery.<br />
<br />
The loaded data can be in Avro, CSV, JSON, ORC, or Parquet format. To create the load job, you can also use the <a href="/bigquery/docs/reference/standard-sql/load-statements"><code dir="ltr" translate="no">        LOAD DATA       </code></a> SQL statement.<br />
<br />
Popular open source systems, such as <a href="/dataproc/docs/tutorials/bigquery-connector-spark-example">Spark</a> and various <a href="/bigquery/docs/bigquery-ready-partners#etl-data-integration">ETL partners</a> , also support batch loading data into BigQuery.<br />
<br />
To optimize batch loading into tables to avoid reaching the daily load limit, see <a href="/bigquery/docs/optimize-load-jobs">Optimize load jobs</a> .</td>
</tr>
<tr class="even">
<td><strong>Streaming load</strong></td>
<td>If you must support custom streaming data sources, or preprocess data before streaming it with large throughput into BigQuery, use <a href="/dataflow/docs">Dataflow</a> .<br />
<br />
For more information about loading from Dataflow to BigQuery, see <a href="/dataflow/docs/guides/write-to-bigquery">Write from Dataflow to BigQuery</a> .<br />
<br />
You can also directly use the <a href="/bigquery/docs/write-api">BigQuery Storage Write API</a> .<br />
<br />
To optimize streaming into tables to avoid reaching the daily load limit, see <a href="/bigquery/docs/optimize-load-jobs">Optimize load jobs</a> .</td>
</tr>
</tbody>
</table>

[Cloud Data Fusion](/data-fusion/docs/concepts/overview) can help facilitate your ETL process. BigQuery also works with [3rd party partners that transform and load data into BigQuery](/bigquery/docs/bigquery-ready-partners#etl-data-integration) .

BigQuery lets you create external connections to query data that's stored outside of BigQuery in Google Cloud services like Cloud Storage or Spanner, or in third-party sources like Amazon Web Services (AWS) or Microsoft Azure. These external connections use the BigQuery Connection API. For more information, see [Introduction to connections](/bigquery/docs/connections-api-intro) .

## Other ways to acquire data

You can run queries on data without loading it into BigQuery yourself. The following sections describe some alternatives.

The following list describes some of the alternatives:

### Run queries on public data

Public datasets are datasets stored in BigQuery and shared with the public. For more information, see [BigQuery public datasets](/bigquery/public-data) .

### Run queries on shared data

To run queries on a BigQuery dataset that someone has shared with you, see [Introduction to BigQuery sharing (formerly Analytics Hub)](/bigquery/docs/analytics-hub-introduction) . Sharing is a data exchange platform that enables data sharing.

### Run queries with log data

You can run queries on logs without creating additional load jobs:

  - **Cloud Logging** lets you [route logs to a BigQuery destination](/logging/docs/export/configure_export) .

  - **Log Analytics** lets you [run queries that analyze your log data](/logging/docs/log-analytics#analytics) .

## What's next

  - Learn how to [prepare data](/bigquery/docs/data-prep-introduction) with Gemini in BigQuery.
  - Learn more about transforming data with [Dataform](/dataform/docs/overview) .
  - Learn more about monitoring load jobs in the [administrative jobs explorer](/bigquery/docs/admin-jobs-explorer) and [BigQuery metrics](/monitoring/api/metrics_gcp_a_b#gcp-bigquery) .
