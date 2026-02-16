# Introduction to tables

A BigQuery table contains individual records organized in rows. Each record is composed of columns (also called *fields* ).

Every table is defined by a *schema* that describes the column names, data types, and other information. You can specify the schema of a table when it is created, or you can create a table without a schema and declare the schema in the query job or load job that first populates it with data.

Use the format `  projectname.datasetname.tablename  ` to fully qualify a table name when using GoogleSQL, or the format `  projectname:datasetname.tablename  ` to fully qualify a table name when using the bq command-line tool.

## Table types

The following sections describe the table types that BigQuery supports.

  - [Standard BigQuery tables](#standard-tables) : structured data stored in BigQuery storage.
  - [External tables](#external_tables) : tables that reference data stored outside BigQuery.
  - [Views](#views) : logical tables that are created by using a SQL query.

### Standard BigQuery tables

Standard BigQuery tables contain structured data and are stored in BigQuery storage in a columnar format. You can also store references to unstructured data in standard tables by using struct columns that adhere to the [`  ObjectRef  `](/bigquery/docs/reference/standard-sql/objectref_functions#objectref) format. For more information about working with `  ObjectRef  ` values, see [Specify ObjectRef columns in table schemas](/bigquery/docs/objectref-columns) .

BigQuery has the following table types:

  - Tables, which have a schema and every column in the schema has a data type.
    
    For information about how to create tables, see [Create tables](/bigquery/docs/tables#create-table) .

  - [Table clones](/bigquery/docs/table-clones-intro) , which are lightweight, writeable copies of BigQuery tables. BigQuery only stores the delta between a table clone and its base table.
    
    For information about how to create table clone, see [Create table clones](/bigquery/docs/table-clones-create) .

  - [Table snapshots](/bigquery/docs/table-snapshots-intro) , which are point-in-time copies of tables. They are read-only, but you can restore a table from a table snapshot. BigQuery stores bytes that are different between a snapshot and its base table, so a table snapshot typically uses less storage than a full copy of the table.
    
    For information about how to create table snapshots, see [Create table snapshots](/bigquery/docs/table-snapshots-create) .

### External tables

External tables are stored outside out of BigQuery storage and refer to data that's stored outside of BigQuery. For more information, see [Introduction to external data sources](/bigquery/docs/external-data-sources) . External tables include the following types:

  - [BigLake tables](/bigquery/docs/biglake-intro) , which reference structured data stored in data stores such as Cloud Storage, Amazon Simple Storage Service (Amazon S3), and Azure Blob Storage. These tables let you enforce fine-grained security at the table level.
    
    For information about how to create BigLake tables, see the following topics:
    
      - [Cloud Storage](/bigquery/docs/query-cloud-storage-using-biglake)
      - [Amazon S3](/bigquery/docs/omni-aws-create-external-table)
      - [Blob Storage](/bigquery/docs/omni-azure-create-external-table)

  - [Object tables](/bigquery/docs/object-table-introduction) , which reference unstructured data stored in data stores such as Cloud Storage.
    
    For information about how to create object tables, see [Create object tables](/bigquery/docs/object-tables) .

  - [Non-BigLake external tables](/bigquery/docs/external-tables) , which reference structured data stored in data stores such as Cloud Storage, Google Drive, and Bigtable. Unlike BigLake tables, these tables don't let you enforce fine-grained security at the table level.
    
    For information about how to create non-BigLake external tables, see the following topics:
    
      - [Cloud Storage](/bigquery/docs/external-data-cloud-storage)
      - [Google Drive](/bigquery/docs/external-data-drive)
      - [Bigtable](/bigquery/docs/external-data-bigtable)

### Views

Views are logical tables that are defined by using a SQL query. These include the following types:

  - [Views](/bigquery/docs/views-intro) , which are logical tables that are defined by using SQL queries. These queries define the view that is run each time the view is queried.
    
    For information about how to create views, see [Create views](/bigquery/docs/views) .

  - [Materialized views](/bigquery/docs/materialized-views-intro) , which are precomputed views that periodically cache the results of the view query. The cached results are stored in BigQuery storage.
    
    For information about how to create materialized views, see [Create materialized views](/bigquery/docs/materialized-views-create) .

## Table limitations

BigQuery tables are subject to the following limitations:

  - Table names must be unique per dataset.
  - When you export BigQuery table data, the only supported destination is Cloud Storage.
  - When you use an API call, enumeration performance slows as you approach 50,000 tables in a dataset.
  - The Google Cloud console can display up to 50,000 tables for each dataset.

For information about BigQuery external table limitations, see the following topics:

  - [BigLake tables](/bigquery/docs/biglake-intro#limitations)
  - [Object tables](/bigquery/docs/object-table-introduction#limitations)
  - [External tables](/bigquery/docs/external-tables#limitations)

## Table quotas

Quotas and limits apply to the different types of jobs you can run against tables, including the following quotas:

  - [Load data into tables](/bigquery/quotas#load_jobs) (load jobs)
  - [Export data from tables](/bigquery/quotas#export_jobs) (extract jobs)
  - [Query table data](/bigquery/quotas#query_jobs) (query jobs)
  - [Copy tables](/bigquery/quotas#copy_jobs) (copy jobs)

For more information about all quotas and limits, see [Quotas and limits](/bigquery/quotas) .

To troubleshoot quota errors for tables, see the [BigQuery Troubleshooting page](/bigquery/docs/troubleshoot-quotas) .

The following quota errors apply specifically to tables:

  - [Table imports or query appends quota errors](/bigquery/docs/troubleshoot-quotas#ts-table-import-quota)
  - [Too many DML statements outstanding against table](/bigquery/docs/troubleshoot-quotas#ts-too-many-dml-statements-against-table-quota)

## Table pricing

When you create and use tables in BigQuery, your charges are based on how much data is stored in the tables and partitions and on the queries you run against the table data:

  - For information about storage pricing, see [Storage pricing](https://cloud.google.com/bigquery/pricing#storage) .
  - For information about query pricing, see [Query pricing](https://cloud.google.com/bigquery/pricing#analysis_pricing_models) .

Many table operations are free, including loading, copying, and exporting data. Though free, these operations are subject to BigQuery [quotas and limits](/bigquery/quotas) . For information about all free operations, see [Free operations](https://cloud.google.com/bigquery/pricing#free) on the pricing page.

## Table security

To control access to tables in BigQuery, see [Control access to resources with IAM](/bigquery/docs/control-access-to-resources-iam) .

## What's next

  - Learn how to [create and use tables](/bigquery/docs/tables) .
  - Learn how to [manage tables](/bigquery/docs/managing-tables) .
  - Learn how to [modify table schemas](/bigquery/docs/managing-table-schemas) .
  - Learn about [working with table data](/bigquery/docs/managing-table-data) .
