# BigQuery interactive walkthroughs and videos

## BigQuery interactive walkthroughs

The following interactive walkthroughs help you get started with BigQuery.

### Before you begin

1.  Enable the BigQuery API.
    
    **Roles required to enable APIs**
    
    To enable APIs, you need the Service Usage Admin IAM role ( `  roles/serviceusage.serviceUsageAdmin  ` ), which contains the `  serviceusage.services.enable  ` permission. [Learn how to grant roles](/iam/docs/granting-changing-revoking-access) .
    
    For new projects, the BigQuery API is automatically enabled.

2.  Optional: [Enable billing](/billing/docs/how-to/modify-project) for the project. If you don't want to enable billing or provide a credit card, the steps in this document still work. BigQuery provides you a sandbox to perform the steps. For more information, see [Enable the BigQuery sandbox](/bigquery/docs/sandbox#setup) .
    
    **Note:** If your project has a billing account and you want to use the BigQuery sandbox, then [disable billing for your project](/billing/docs/how-to/modify-project#disable_billing_for_a_project) .

These walkthroughs are launched in the Google Cloud console. Click the links to launch the interactive tutorial.

<table>
<thead>
<tr class="header">
<th><p>Title</p></th>
<th><p>Description</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>Loading and querying data</strong></td>
<td></td>
</tr>
<tr class="even">
<td><a href="https://console.cloud.google.com/welcome?walkthrough_id=bigquery--bigquery-quickstart-query-public-dataset">Query a public dataset in BigQuery Studio</a></td>
<td>Use the BigQuery sandbox to query and visualize data in a public dataset.</td>
</tr>
<tr class="odd">
<td><a href="https://console.cloud.google.com/welcome?walkthrough_id=bigquery--bigquery-quickstart-load-data-console">Load and query data using BigQuery Studio</a></td>
<td>Use BigQuery Studio to create a dataset, load data, and query the data.</td>
</tr>
<tr class="even">
<td><a href="https://console.cloud.google.com/welcome?walkthrough_id=bigquery--load-data-bq">Load and query data with the <code dir="ltr" translate="no">        bq       </code> command-line tool</a></td>
<td>Use the BigQuery command-line tool to create a dataset, load data, and query the data.</td>
</tr>
<tr class="odd">
<td><a href="https://console.cloud.google.com/welcome?tutorial=bigquery_import_data_from_cloud_storage">Import data from Cloud Storage to BigQuery</a></td>
<td>Use the Google Cloud console to import data from Cloud Storage into BigQuery, and query the data.</td>
</tr>
<tr class="even">
<td><strong>Workload management</strong></td>
<td></td>
</tr>
<tr class="odd">
<td><a href="https://console.cloud.google.com/welcome?walkthrough_id=bigquery--reservations-get-started">Get started with reservations</a></td>
<td>Use the Google Cloud console to purchase slots, create a reservation, and assign a project to a reservation.</td>
</tr>
<tr class="even">
<td><strong>AI</strong></td>
<td></td>
</tr>
<tr class="odd">
<td><a href="https://console.cloud.google.com/bigquery?walkthrough_id=bigquery--write-sql-gemini">Write queries with Gemini assistance</a></td>
<td>Use Gemini AI-powered assistance in BigQuery to help you query your data using SQL queries and Python code.</td>
</tr>
<tr class="even">
<td><strong>Client libraries</strong></td>
<td></td>
</tr>
<tr class="odd">
<td><a href="https://console.cloud.google.com/?walkthrough_id=bigquery--csharp-client-library">C# tour</a></td>
<td>Query a public dataset with the BigQuery C# client library.</td>
</tr>
<tr class="even">
<td><a href="https://console.cloud.google.com/?walkthrough_id=bigquery--go-client-library">Go tour</a></td>
<td>Query a public dataset with the BigQuery Go client library.</td>
</tr>
<tr class="odd">
<td><a href="https://console.cloud.google.com/?walkthrough_id=bigquery--java-client-library">Java tour</a></td>
<td>Query a public dataset with the BigQuery Java client library.</td>
</tr>
<tr class="even">
<td><a href="https://console.cloud.google.com/?walkthrough_id=bigquery--node-client-library">Node.js tour</a></td>
<td>Query a public dataset with the BigQuery Node.js client library.</td>
</tr>
<tr class="odd">
<td><a href="https://console.cloud.google.com/?walkthrough_id=bigquery--php-client-library">PHP tour</a></td>
<td>Query a public dataset with the BigQuery PHP client library.</td>
</tr>
<tr class="even">
<td><a href="https://console.cloud.google.com/?walkthrough_id=bigquery--python-client-library">Python tour</a></td>
<td>Query a public dataset with the BigQuery Python client library.</td>
</tr>
<tr class="odd">
<td><a href="https://console.cloud.google.com/?walkthrough_id=bigquery--ruby-client-library">Ruby tour</a></td>
<td>Query a public dataset with the BigQuery Ruby client library.</td>
</tr>
</tbody>
</table>

## BigQuery videos

The following series of video tutorials help you learn more about BigQuery. For more Google Cloud videos, subscribe to the [Google Cloud Tech](https://goo.gle/GoogleCloudTech) YouTube channel.

<table>
<thead>
<tr class="header">
<th><p>Title</p></th>
<th><p>Description</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>Product overviews</strong></td>
<td></td>
</tr>
<tr class="even">
<td><a href="https://www.youtube.com/watch?v=CFw4peH2UwU">BigQuery in a minute</a> (1:26)</td>
<td>A brief overview of BigQuery, Google's fully-managed data warehouse.</td>
</tr>
<tr class="odd">
<td><a href="https://www.youtube.com/watch?v=0RMT8uEplbM">BigQuery ML in a minute</a> (1:40)</td>
<td>A brief overview of BigQuery ML. With BigQuery ML, you can train, evaluate, and run inference on models for tasks such as time series forecasting, anomaly detection, classification, regression, clustering, dimensionality reduction, and recommendations.</td>
</tr>
<tr class="even">
<td><strong>AI</strong></td>
<td></td>
</tr>
<tr class="odd">
<td><a href="https://www.youtube.com/watch?v=-MWIHAH4cbA">Introduction to Gemini AI and data analytics in BigQuery</a> (3:42)</td>
<td>An introduction to Gemini in BigQuery, which provides AI and data analytics capabilities that help streamline your workflows across the entire data lifecycle.</td>
</tr>
<tr class="even">
<td><a href="https://www.youtube.com/watch?v=qrT4g0hZHns">Use BigQuery &amp; Gemini AI for data analytics</a> (7:00)</td>
<td>An overview of how Gemini models can help you generate new insights, enrich your datasets, and even analyze multimodal content including images, videos, and text.</td>
</tr>
<tr class="odd">
<td><a href="https://www.youtube.com/watch?v=SqjGq275d0M">Introducing BigQuery data engineering agents</a> (6:19)</td>
<td>An introduction to BigQuery Data Engineering Agents that help data analysts save time coding, schema mapping, and creating metadata.</td>
</tr>
<tr class="even">
<td><a href="https://www.youtube.com/watch?v=r_nDZSrWaYk">BigQuery data canvas overview</a> (6:03)</td>
<td>An overview of AI-powered BigQuery data canvas. This natural language centric tool simplifies the process of finding, querying, and visualizing your data.</td>
</tr>
<tr class="odd">
<td><strong>Querying and visualizing data</strong></td>
<td></td>
</tr>
<tr class="even">
<td><a href="https://www.youtube.com/watch?v=mW2CLYr6w4M">Introducing pipe syntax in BigQuery and Cloud Logging</a> (5:00)</td>
<td>BigQuery's pipe syntax offers a more intuitive way to structure your code. Learn how pipe syntax simplifies both exploratory analysis and complex log analytics tasks, helping you gain insights faster.</td>
</tr>
<tr class="odd">
<td><a href="https://www.youtube.com/watch?v=t_q-qLa1lX0">Visualizing BigQuery geospatial data in Colab</a> (10:00)</td>
<td>BigQuery lets you store and analyze geospatial data using standard SQL, and bringing that data into a Colab notebook gives you the flexibility to combine BigQuery's power with popular Python visualization libraries.</td>
</tr>
<tr class="even">
<td><a href="https://www.youtube.com/watch?v=Q2JD3_YBaRc">Visualize BigQuery data with Looker</a> (3:00)</td>
<td>An overview of how to seamlessly connect to and visualize your BigQuery data using Looker's user-friendly interface and powerful semantic modeling capabilities.</td>
</tr>
<tr class="odd">
<td><strong>BigQuery storage</strong></td>
<td></td>
</tr>
<tr class="even">
<td><a href="https://www.youtube.com/watch?v=V2QTtHJXVZY">A tour of BigQuery tables</a> (6:55)</td>
<td>An overview of the different types of tables in BigQuery, including managed tables, external tables, and virtual tables with logical and materialized views.</td>
</tr>
<tr class="odd">
<td><a href="https://www.youtube.com/watch?v=0Hd23GnZ1bE">How does BigQuery store data?</a> (8:19)</td>
<td>An introduction to how BigQuery stores data so you can make informed decisions on how to optimize your BigQuery storage. This includes an overview of partitioning and clustering.</td>
</tr>
<tr class="even">
<td><strong>Monitoring and logging</strong></td>
<td></td>
</tr>
<tr class="odd">
<td><a href="https://www.youtube.com/watch?v=UY_jy02jBoI">Monitoring in BigQuery</a> (7:43)</td>
<td>An overview of how monitoring your data warehouse can optimize costs, help you pinpoint which queries need to be optimized, and audit both data sharing and access.</td>
</tr>
</tbody>
</table>
