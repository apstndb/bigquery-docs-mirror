# Manage BigQuery API dependencies

This document describes the Google Cloud services and APIs that BigQuery depends on. It also explains the effects on BigQuery behavior when you disable those services. Review this document before you enable or disable services in your project.

Some services are enabled by default in every Google Cloud project that you create. Other APIs are automatically enabled for all Google Cloud projects that use BigQuery. The remaining services must be explicitly enabled before you can use their functionality. For more information, see the following resources:

  - [Services enabled by default](/service-usage/docs/enabled-service#default)
  - [Enabling and disabling services](/service-usage/docs/enable-disable)

This document is intended for administrators.

## Services enabled by default

The following services are enabled by default for every new Google Cloud project:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Service</strong></th>
<th><strong>Which features rely on it</strong></th>
<th><strong>Effects of disabling this service</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       analyticshub.googleapis.com      </code></td>
<td><ul>
<li><a href="/bigquery/docs/analytics-hub-introduction">Publish data exchanges</a></li>
<li><a href="/bigquery/docs/analytics-hub-manage-listings">Publish listings</a> and <a href="/bigquery/docs/analytics-hub-manage-subscriptions">manage subscriptions</a></li>
<li><a href="/bigquery/docs/data-clean-rooms">Data clean rooms</a></li>
</ul></td>
<td><ul>
<li>You can't create or manage data exchanges, listings, data clean rooms, or subscriptions.</li>
<li>You can't search and explore exchanges or listings that other providers create.</li>
<li>Created subscriptions persist but aren't accessible.</li>
<li>Linked datasets are accessible as long as the BigQuery API is enabled.</li>
<li>You can't create new subscriptions</li>
</ul></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       bigqueryconnection.googleapis.com      </code></td>
<td><ul>
<li><a href="/bigquery/docs/federated-queries-intro">Federated queries</a> to data stored outside of BigQuery</li>
<li>External tables and datasets</li>
<li><a href="/bigquery/docs/about-bqms">BigQuery metastore</a></li>
</ul></td>
<td><ul>
<li>You can't manage external connections.</li>
<li>You can't create remote models.</li>
<li>You can't create remote functions.</li>
<li>You can't query BigLake tables and object tables.</li>
</ul></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       bigquerymigration.googleapis.com      </code></td>
<td><ul>
<li><a href="/bigquery/docs/migration-assessment">Data migration assessment</a></li>
<li><a href="/bigquery/docs/interactive-sql-translator">SQL query translation</a></li>
</ul></td>
<td><ul>
<li>You can't create migration tasks or assessments.</li>
<li>Existing tasks or assessments aren't available.</li>
</ul>
<p><strong>Note:</strong> Usually you can disable this service after completing data migration.</p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       bigquerydatapolicy.googleapis.com      </code></td>
<td><ul>
<li><a href="/bigquery/docs/column-data-masking-intro">Data masking</a></li>
</ul></td>
<td><ul>
<li>You can't manage your data masking policies.</li>
<li>Data masking policies aren't deleted, but queries to tables with data masking applied fail.</li>
</ul></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       bigquerydatatransfer.googleapis.com      </code></td>
<td><ul>
<li><a href="/bigquery/docs/dts-introduction">Scheduled data transfers</a></li>
</ul></td>
<td><ul>
<li>You can't manage your scheduled data transfers.</li>
<li>Existing data transfers stop.</li>
</ul></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       bigqueryreservation.googleapis.com      </code></td>
<td><ul>
<li><a href="/bigquery/docs/reservations-get-started">Capacity-based workload management</a></li>
</ul></td>
<td><ul>
<li>You can't create or manage capacity commitments, reservations, or assignments.</li>
<li>You can't monitor slot usage.</li>
<li>Disaster recovery failover isn't available.</li>
<li>Slot autoscaling stops.</li>
</ul></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       bigquerystorage.googleapis.com      </code></td>
<td><ul>
<li><a href="/bigquery/docs/write-api-streaming">Streaming data ingestion</a></li>
<li><a href="/bigquery/docs/write-api-batch">Batch data loading</a></li>
<li><a href="/bigquery/docs/change-data-capture">Change data capture</a></li>
</ul></td>
<td><ul>
<li>You can't use the <a href="/bigquery/docs/reference/storage">Storage Read API</a> or the <a href="/bigquery/docs/write-api">Storage Write API</a> to access your BigQuery data.</li>
</ul></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       dataform.googleapis.com      </code></td>
<td>Dataform provides code repositories that are leveraged by the following features:
<ul>
<li><a href="/dataform/docs/quickstart-create-workflow">BigQuery pipelines</a></li>
<li><a href="/bigquery/docs/work-with-saved-queries">Saved queries</a></li>
<li><a href="/bigquery/docs/notebooks-introduction">Colab notebooks</a></li>
<li><a href="/dataform/docs">Dataform</a></li>
<li><a href="/bigquery/docs/data-prep-introduction">Data preparation</a></li>
<li><a href="/bigquery/docs/data-canvas">Data canvas</a></li>
</ul></td>
<td><ul>
<li>You can't create pipelines, saved queries, Colab notebooks, data canvases, data preparations, or Dataform projects.</li>
<li>Existing scheduled pipelines, notebooks, or Dataform projects stop.</li>
<li>Any existing pipelines, saved queries, Colab notebooks, data canvases, data preparations, or Dataform projects become inaccessible.</li>
</ul></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       dataplex.googleapis.com      </code></td>
<td><ul>
<li>Dataplex Universal Catalog provides data cataloging and governance capabilities that are used by the following:
<ul>
<li>Resource Explorer in BigQuery Studio</li>
<li>Autocomplete in BigQuery Studio SQL editor</li>
<li><a href="/bigquery/docs/analytics-hub-view-subscribe-listings">BigQuery sharing (formerly Analytics Hub) search for listings</a></li>
<li><a href="/bigquery/docs/data-profile-scan">Profile insights</a></li>
<li><a href="/bigquery/docs/data-quality-scan">Data quality scans</a></li>
<li><a href="/dataplex/docs/use-lineage#view-bq-lineage">Data lineage</a> viewing</li>
<li><a href="/bigquery/docs/data-insights">Table and dataset insights</a></li>
<li><a href="/bigquery/docs/data-canvas">Data canvas</a></li>
</ul></li>
</ul></td>
<td><ul>
<li>BigQuery data asset search is unavailable.</li>
<li>Sharing listing search is unavailable.</li>
<li>You can't create new or access previously created profile insights, data quality scans, or query suggestions.</li>
<li>You can't see data asset details on a lineage graph.</li>
<li>You can't search for data assets in data canvas.</li>
</ul></td>
</tr>
</tbody>
</table>

### Effect of disabling the BigQuery API

Disabling the BigQuery API also disables the following services which are dependent upon BigQuery API:

  - binaryauthorization.googleapis.com
  - container.googleapis.com
  - cloudapis.googleapis.com
  - dataprep.googleapis.com
  - servicebroker.googleapis.com
  - telecomdatafabric.googleapis.com

## Services enabled by BigQuery Unified API

The BigQuery Unified API ( `  bigqueryunified.googleapis.com  ` ) includes a curated collection of services that are required for various BigQuery features to function. If you enable the BigQuery Unified API, then all of these services are activated simultaneously. Google can update the services in this collection, and those services are automatically enabled in projects with this API enabled. You can disable individual services and APIs.

For instructions on enabling `  bigqueryunified.googleapis.com  ` , see [Enabling and disabling services](/service-usage/docs/enable-disable) .

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Service</strong></th>
<th><strong>Which features rely on it</strong></th>
<th><strong>Effects of disabling this service</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       aiplatform.googleapis.com      </code></td>
<td><ul>
<li><a href="/bigquery/docs/notebooks-introduction">Colab notebooks</a></li>
<li><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model">BigQuery ML remote models</a></li>
</ul></td>
<td><ul>
<li>You won't be able to run your notebooks.</li>
<li>Any existing BigQuery ML remote models stop working.</li>
<li>Your existing notebooks remain accessible for editing.</li>
</ul></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       bigqueryunified.googleapis.com      </code></td>
<td><ul>
<li>Provides a single-click activation of the BigQuery dependent services listed in this document, excluding the <strong>cloudaicompanion</strong> , <strong>composer</strong> and <strong>datalineage</strong> APIs.</li>
<li>Ensures new BigQuery dependencies are enabled in your project.</li>
</ul></td>
<td><ul>
<li>Future dependencies aren't automatically enabled in your project.</li>
</ul></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       compute.googleapis.com      </code></td>
<td><ul>
<li>Google Compute Engine provides a runtime environment for all features provided by Dataproc and Vertex AI.</li>
</ul></td>
<td><ul>
<li>Colab notebooks, remote ML models, Apache Spark, SparkSQL, and PySpark jobs stop.</li>
<li>Source code remains available.</li>
<li>Dataproc API gets disabled.</li>
</ul></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       dataproc.googleapis.com      </code></td>
<td><ul>
<li><a href="/bigquery/docs/bqms-use-dataproc">Query data with open source engines such as Apache Spark.</a></li>
<li><a href="/bigquery/docs/bqms-use-dataproc-serverless">Use Spark SQL or PySpark with Google Cloud Serverless for Apache Spark.</a></li>
<li><a href="/bigquery/docs/spark-procedures">Use stored procedures for Spark.</a></li>
</ul></td>
<td><ul>
<li>You can't create Dataproc clusters to run open source data analytics.</li>
<li>You can't run Serverless for Apache Spark workloads.</li>
<li>You can't run Spark in BigQuery workloads.</li>
</ul></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       datastream.googleapis.com      </code></td>
<td><ul>
<li><a href="/datastream/docs/overview">Provides change data capture and replication to BigQuery.</a></li>
</ul></td>
<td><ul>
<li>All data streams are paused and aren't accessible.</li>
</ul></td>
</tr>
</tbody>
</table>

## Services disabled by default

You must manually enable the following services for the corresponding capabilities to become available:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Service</strong></th>
<th><strong>Which features rely on it</strong></th>
<th><strong>Effects of disabling this service</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       cloudaicompanion.googleapis.com      </code></td>
<td><ul>
<li>Gemini in BigQuery features</li>
</ul></td>
<td><ul>
<li><p>Code completion, generation, and explanation features stop working.</p>
<p>Learn more about <a href="/bigquery/docs/gemini-set-up#turn-off">turning off Gemini in BigQuery</a> .</p></li>
</ul></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       composer.googleapis.com      </code></td>
<td><ul>
<li><a href="/bigquery/docs/orchestrate-workloads">Schedule workloads</a></li>
</ul></td>
<td><ul>
<li>Existing Cloud Composer DAGs aren't listed on the Scheduling page and stop.</li>
<li>Existing Cloud Composer environments become inoperative, stop working, and return an error state.</li>
</ul></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       datalineage.googleapis.com      </code></td>
<td><ul>
<li><a href="/dataplex/docs/use-lineage#view-bq-lineage">Data lineage</a> capture and viewing</li>
</ul></td>
<td><ul>
<li>Data lineage isn't captured for your project.</li>
<li>You can't view the lineage graph.</li>
</ul></td>
</tr>
</tbody>
</table>

## Manually enable BigQuery code assets

To manage code assets in BigQuery, such as notebooks and saved queries, you must enable the following APIs:

  - The Compute Engine API
  - The Dataform API
  - The Vertex AI API

Before March 2024, these APIs were not automatically enabled by default. If you have automation scripts from before March 2024 that depended on the status of these APIs, then you might need to update them. If you already have these APIs enabled, then you will see new **Notebooks** and **Queries** folders in the **Explorer** pane in BigQuery.

### Before you begin

To manually enable code asset management, you must have the Identity and Access Management (IAM) [Owner role](/iam/docs/roles-overview#legacy-basic) ( `  roles/owner  ` ) .

### Manually enable BigQuery code assets

To enable required API dependencies for code assets, follow these steps:

1.  Go to the **BigQuery** page.

2.  On the **Studio** , in the tab bar of the editor pane, click the arrow\_drop\_down arrow drop-down next to the **+** sign, hold the pointer over **Notebook** , and then select **Empty notebook** .

3.  Click **Enable APIs** .
    
    If you don't see this option, check if you have the required IAM [Owner role](/iam/docs/roles-overview#legacy-basic) ( `  roles/owner  ` ). If an empty notebook opens, then you already have the necessary APIs enabled.

4.  In the **Enable core features** pane, in the **Core feature APIs** section, do the following:
    
    1.  To enable all BigQuery dependencies for data streaming, scheduling, and notebooks, next to **BigQuery Unified API** click **Enable** .
    2.  Optional: To choose which APIs to enable, click **View and enable individual APIs** and then click **Enable** next to each API that you want to enable.
    3.  When the APIs are enabled, click **Next** .

5.  Optional: Set user permissions in the **Permissions** section:
    
      - To grant principals the ability to create code assets, and to read, edit, and set permissions for the code assets they created, type their user or group names in the **BigQuery Studio User** field.
      - To grant principals the ability to read, edit, and set permissions for all code assets shared with them, type their user or group names in the **BigQuery Studio Admin** field.

6.  Click **Next** .

7.  Optional: In the **Additional APIs** section, click **Enable all** to enable the APIs that you need to create BigQuery remote procedures by using [BigQuery DataFrames](/python/docs/reference/bigframes/latest) .

8.  If you chose not to enable the additional APIs, click **Close** to close the **Enable core features** pane.

### Restrict access to code assets

You can help prevent enablement of additional APIs by setting the [Restrict Resource Service Usage organization policy constraint](/resource-manager/docs/organization-policy/restricting-resources) . You can [turn off selected APIs](/service-usage/docs/enable-disable#disabling) at any time.

## What's next?

  - To learn how to manage Google Cloud services, see [Enabling and disabling services](/service-usage/docs/enable-disable) .
  - To learn how to manage API access at a granular level with organization policy constraints, see [Restricting resource usage](/resource-manager/docs/organization-policy/restricting-resources) .
  - To learn how to control access to services with Identity and Access Management (IAM) roles and permissions for BigQuery, see [BigQuery IAM roles and permissions](/bigquery/docs/access-control) .
