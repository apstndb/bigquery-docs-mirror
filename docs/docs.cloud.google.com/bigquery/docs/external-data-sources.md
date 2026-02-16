# Introduction to external data sources

This page provides an overview of querying data stored outside of BigQuery.

An external data source is a data source that you can query directly from BigQuery, even though the data is not stored in BigQuery storage. For example, you might have data in a different Google Cloud database, in files in Cloud Storage, or in a different cloud product altogether that you would like to analyze in BigQuery, but that you aren't prepared to migrate.

Use cases for external data sources include the following:

  - For extract-load-transform (ELT) workloads, loading and cleaning your data in one pass and writing the cleaned result into BigQuery storage, by using a `  CREATE TABLE ... AS SELECT  ` query.
  - Joining BigQuery tables with frequently changing data from an external data source. By querying the external data source directly, you don't need to reload the data into BigQuery storage every time it changes.

BigQuery has two different mechanisms for querying external data: external tables and federated queries.

## External tables

External tables are similar to standard BigQuery tables, in that these tables store their metadata and schema in BigQuery storage. However, their data resides in an external source.

External tables are contained inside a dataset, and you manage them in the same way that you manage a standard BigQuery table. For example, you can [view the table's properties](/bigquery/docs/tables#get_information_about_tables) , [set access controls](/bigquery/docs/table-access-controls) , and so forth. You can query these tables and in most cases you can join them with other tables.

There are four kinds of external tables:

  - BigLake tables
  - BigQuery Omni tables
  - Object tables
  - Non-BigLake external tables

### BigLake tables

BigLake tables let you query structured data in external data stores with access delegation. Access delegation decouples access to the BigLake table from access to the underlying data store. An [external connection](/bigquery/docs/connections-api-intro) associated with a service account is used to connect to the data store. Because the service account handles retrieving data from the data store, you only have to grant users access to the BigLake table. This lets you enforce fine-grained security at the table level, including [row-level](/bigquery/docs/row-level-security-intro) and [column-level](/bigquery/docs/column-level-security-intro) security. For BigLake tables based on Cloud Storage, you can also use [dynamic data masking](/bigquery/docs/column-data-masking) . To learn more about multi-cloud analytic solutions using BigLake tables with Amazon S3 or Blob Storage data, see [BigQuery Omni](/bigquery/docs/omni-introduction) .

For more information, see [Introduction to BigLake tables](/bigquery/docs/biglake-intro) .

### Object tables

Object tables let you analyze unstructured data in Cloud Storage. You can perform analysis with remote functions or perform inference by using BigQuery ML, and then join the results of these operations with the rest of your structured data in BigQuery.

Like BigLake tables, object tables use access delegation, which decouples access to the object table from access to the Cloud Storage objects. An [external connection](/bigquery/docs/working-with-connections) associated with a service account is used to connect to Cloud Storage, so you only have to grant users access to the object table. This lets you enforce [row-level](/bigquery/docs/row-level-security-intro) security and manage which objects users have access to.

For more information, see [Introduction to object tables](/bigquery/docs/object-table-introduction) .

### Non-BigLake external tables

Non-BigLake external tables let you query structured data in external data stores. To query a non-BigLake external table, you must have permissions to both the external table and the external data source. For example, to query a non-BigLake external table that uses a data source in Cloud Storage, you must have the following permissions:

  - `  bigquery.tables.getData  `
  - `  bigquery.jobs.create  `
  - `  storage.buckets.get  `
  - `  storage.objects.get  `

For more information, see [Introduction to external tables](/bigquery/docs/external-tables) .

## Federated queries

Federated queries let you send a query statement to AlloyDB, Spanner, or Cloud SQL databases and get the result back as a temporary table. Federated queries use the BigQuery Connection API to establish a connection with AlloyDB, Spanner, or Cloud SQL. In your query, you use the `  EXTERNAL_QUERY  ` function to send a query statement to the external database, using that database's SQL dialect. The results are converted to GoogleSQL data types.

For more information, see [Introduction to federated queries](/bigquery/docs/federated-queries-intro) .

## External data source feature comparison

The following table compares the behavior of external data sources:

<table>
<thead>
<tr class="header">
<th></th>
<th><strong>BigLake tables</strong></th>
<th><strong>Object tables</strong></th>
<th><strong>Non-BigLake external tables</strong></th>
<th><strong>Federated queries</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>Uses access delegation</strong></td>
<td>Yes, through a service account</td>
<td>Yes, through a service account</td>
<td>No</td>
<td>Yes, through a database user account (Cloud SQL only)</td>
</tr>
<tr class="even">
<td><strong>Can be based on multiple source URIs</strong></td>
<td>Yes</td>
<td>Yes</td>
<td>Yes (Cloud Storage only)</td>
<td>Not applicable</td>
</tr>
<tr class="odd">
<td><strong>Row mapping</strong></td>
<td>Rows represent file content</td>
<td>Rows represent file metadata</td>
<td>Rows represent file content</td>
<td>Not applicable</td>
</tr>
<tr class="even">
<td><strong>Accessible by other data processing tools by using connectors</strong></td>
<td>Yes (Cloud Storage only)</td>
<td>No</td>
<td>Yes</td>
<td>Not applicable</td>
</tr>
<tr class="odd">
<td><strong>Can be joined to other BigQuery tables</strong></td>
<td>Yes (Cloud Storage only)</td>
<td>Yes</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr class="even">
<td><strong>Can be accessed as a temporary table</strong></td>
<td>Yes (Cloud Storage only)</td>
<td>No</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><strong>Works with Amazon S3</strong></td>
<td><a href="/bigquery/docs/omni-aws-introduction">Yes</a></td>
<td>No</td>
<td>No</td>
<td>No</td>
</tr>
<tr class="even">
<td><strong>Works with Azure Storage</strong></td>
<td><a href="/bigquery/docs/omni-azure-introduction">Yes</a></td>
<td>No</td>
<td>No</td>
<td>No</td>
</tr>
<tr class="odd">
<td><strong>Works with Bigtable</strong></td>
<td>No</td>
<td>No</td>
<td><a href="/bigquery/docs/external-data-bigtable">Yes</a></td>
<td>No</td>
</tr>
<tr class="even">
<td><strong>Works with Spanner</strong></td>
<td>No</td>
<td>No</td>
<td>No</td>
<td><a href="/bigquery/docs/spanner-federated-queries">Yes</a></td>
</tr>
<tr class="odd">
<td><strong>Works with Cloud SQL</strong></td>
<td>No</td>
<td>No</td>
<td>No</td>
<td><a href="/bigquery/docs/cloud-sql-federated-queries">Yes</a></td>
</tr>
<tr class="even">
<td><strong>Works with Google Drive</strong></td>
<td>No</td>
<td>No</td>
<td><a href="/bigquery/docs/external-data-drive">Yes</a></td>
<td>No</td>
</tr>
<tr class="odd">
<td><strong>Works with Cloud Storage</strong></td>
<td><a href="/bigquery/docs/query-cloud-storage-using-biglake">Yes</a></td>
<td><a href="/bigquery/docs/object-tables">Yes</a></td>
<td><a href="/bigquery/docs/external-data-cloud-storage">Yes</a></td>
<td>No</td>
</tr>
</tbody>
</table>

## What's next

  - Learn more about [BigLake tables](/bigquery/docs/biglake-intro) .
  - Learn more about [object tables](/bigquery/docs/object-table-introduction)
  - Learn more about [external tables](/bigquery/docs/external-tables) .
  - Learn more about [federated queries](/bigquery/docs/federated-queries-intro) .
  - Learn about [BigQuery pricing](https://cloud.google.com/bigquery/pricing#on_demand_pricing) .
