---
name: documents/docs.cloud.google.com/bigquery/docs/enable-sql-translations
uri: https://docs.cloud.google.com/bigquery/docs/enable-sql-translations
title: Enable SQL translations for BigQuery migrations
description: Describes how
data_source: docs.cloud.google.com
---

# Enable SQL translations for BigQuery migrations

As you migrate from your data warehouses to BigQuery, use the BigQuery SQL translators to translate SQL scripts and queries from the source dialect into GoogleSQL.

BigQuery offers the following SQL translation as part of the BigQuery Migration Service:

  - [Interactive SQL translator](https://docs.cloud.google.com/bigquery/docs/interactive-sql-translator)
  - [Translation API](https://docs.cloud.google.com/bigquery/docs/api-sql-translator)
  - [Batch SQL translator](https://docs.cloud.google.com/bigquery/docs/batch-sql-translator)

Before you translate your source SQL, we recommend that you [use the `dwh-migration-dumper` tool to extract DDL schema metadata from your source data warehouses](https://docs.cloud.google.com/bigquery/docs/generate-metadata) . The extracted metadata can be used with the SQL translators to improve SQL translation accuracy.

This document shows you the required steps to take before you can use any of the SQL translators. This document also shows you the SQL dialects supported by the SQL translators, and the regions where SQL translation is supported.

## Enable SQL translations

Before you translate your SQL using the SQL translators, do the following steps.

### Enable the BigQuery Migration API

If your Google Cloud CLI project was created before February 15, 2022, enable the BigQuery Migration API by doing the following:

1.  In the Google Cloud console, go to the **BigQuery Migration API** page.

2.  Click **Enable** .

> **Note:** Projects created after February 15, 2022 have this API enabled automatically.

### Add the required permissions

To get the permissions that you need to create translation jobs with the interactor translator, the translation API, or the batch SQL translator, ask your administrator to grant you the following IAM roles on the `parent` resource:

  - Viewing and monitoring migration jobs: [MigrationWorkflow Viewer](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerymigration#bigquerymigration.viewer) ( `roles/bigquerymigration.viewer` )
  - Submitting migration jobs: [MigrationWorkflow Editor](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerymigration#bigquerymigration.editor) ( `roles/bigquerymigration.editor` )
  - Access the Cloud Storage buckets for input and files: Storage Object Admin ( `roles/storage.objectAdmin` ) - on the source and destination Cloud Storage bucket.

For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

These predefined roles contain the permissions required to create translation jobs with the interactor translator, the translation API, or the batch SQL translator. To see the exact permissions that are required, expand the **Required permissions** section:

#### Required permissions

The following permissions are required to create translation jobs with the interactor translator, the translation API, or the batch SQL translator:

  - `bigquerymigration.workflows.create`
  - `bigquerymigration.workflows.get`
  - `bigquerymigration.workflows.list`
  - `bigquerymigration.workflows.delete`
  - `bigquerymigration.subtasks.get`
  - `bigquerymigration.subtasks.list`
  - `storage.objects.get`
  - `storage.objects.list`
  - `storage.objects.create`

You might also be able to get these permissions with [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

## Supported SQL dialects

The BigQuery SQL translators supports the translations of the following SQL dialects into GoogleSQL:

  - Amazon Redshift SQL ( `Redshift2BigQuery_Translation` )
  - Apache HiveQL and Beeline CLI ( `HiveQL2BigQuery_Translation` )
  - IBM Netezza SQL and NZPLSQL ( `Netezza2BigQuery_Translation` )
  - Snowflake SQL ( `Snowflake2BigQuery_Translation` )
  - Teradata and Teradata Vantage ( `Teradata2BigQuery_Translation` )
      - SQL
      - Basic Teradata Query (BTEQ)
      - Teradata Parallel Transport (TPT)

Additionally, translation of the following SQL dialects is supported in [preview](https://cloud.google.com/products/#product-launch-stages) :

  - Apache Impala SQL ( `Impala2BigQuery_Translation` )
  - Apache Spark SQL ( `SparkSQL2BigQuery_Translation` )
  - Azure Synapse T-SQL ( `AzureSynapse2BigQuery_Translation` )
  - GoogleSQL, BigQuery ( `Bigquery2Bigquery_Translation` )
  - Greenplum SQL ( `Greenplum2BigQuery_Translation` )
  - IBM DB2 SQL ( `Db22BigQuery_Translation` )
  - MySQL SQL ( `MySQL2BigQuery_Translation` )
  - Oracle SQL, PL/SQL, Exadata ( `Oracle2BigQuery_Translation` )
  - PostgreSQL SQL ( `Postgresql2BigQuery_Translation` )
  - Trino or PrestoSQL ( `Presto2BigQuery_Translation` )
  - SQL Server T-SQL ( `SQLServer2BigQuery_Translation` )
  - SQLite ( `SQLite2BigQuery_Translation` )
  - Vertica SQL ( `Vertica2BigQuery_Translation` )

## Locations

The BigQuery SQL translators are available in the following processing locations:

**Region description**

**Region name**

**Details**

**Asia Pacific**

Bangkok

`asia-southeast3`

Delhi

`asia-south2`

Hong Kong

`asia-east2`

Jakarta

`asia-southeast2`

Melbourne

`australia-southeast2`

Mumbai

`asia-south1`

Osaka

`asia-northeast2`

Seoul

`asia-northeast3`

Singapore

`asia-southeast1`

Sydney

`australia-southeast1`

Taiwan

`asia-east1`

Tokyo

`asia-northeast1`

**Europe**

Belgium

`europe-west1`

![leaf icon](https://cloud.google.com/sustainability/region-carbon/gleaf.svg) [Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker)

Berlin

`europe-west10`

EU multi-region

`eu`

Finland

`europe-north1`

![leaf icon](https://cloud.google.com/sustainability/region-carbon/gleaf.svg) [Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker)

Frankfurt

`europe-west3`

London

`europe-west2`

![leaf icon](https://cloud.google.com/sustainability/region-carbon/gleaf.svg) [Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker)

Madrid

`europe-southwest1`

![leaf icon](https://cloud.google.com/sustainability/region-carbon/gleaf.svg) [Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker)

Milan

`europe-west8`

Netherlands

`europe-west4`

![leaf icon](https://cloud.google.com/sustainability/region-carbon/gleaf.svg) [Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker)

Paris

`europe-west9`

![leaf icon](https://cloud.google.com/sustainability/region-carbon/gleaf.svg) [Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker)

Stockholm

`europe-north2`

![leaf icon](https://cloud.google.com/sustainability/region-carbon/gleaf.svg) [Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker)

Turin

`europe-west12`

Warsaw

`europe-central2`

Zürich

`europe-west6`

![leaf icon](https://cloud.google.com/sustainability/region-carbon/gleaf.svg) [Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker)

**Americas**

Columbus, Ohio

`us-east5`

Dallas

`us-south1`

![leaf icon](https://cloud.google.com/sustainability/region-carbon/gleaf.svg) [Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker)

Iowa

`us-central1`

![leaf icon](https://cloud.google.com/sustainability/region-carbon/gleaf.svg) [Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker)

Las Vegas

`us-west4`

Los Angeles

`us-west2`

Mexico

`northamerica-south1`

Northern Virginia

`us-east4`

Oregon

`us-west1`

![leaf icon](https://cloud.google.com/sustainability/region-carbon/gleaf.svg) [Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker)

Québec

`northamerica-northeast1`

![leaf icon](https://cloud.google.com/sustainability/region-carbon/gleaf.svg) [Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker)

São Paulo

`southamerica-east1`

![leaf icon](https://cloud.google.com/sustainability/region-carbon/gleaf.svg) [Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker)

Salt Lake City

`us-west3`

Santiago

`southamerica-west1`

![leaf icon](https://cloud.google.com/sustainability/region-carbon/gleaf.svg) [Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker)

South Carolina

`us-east1`

Toronto

`northamerica-northeast2`

![leaf icon](https://cloud.google.com/sustainability/region-carbon/gleaf.svg) [Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker)

US multi-region

`us`

**Africa**

Johannesburg

`africa-south1`

**MiddleEast**

Dammam

`me-central2`

Doha

`me-central1`

Israel

`me-west1`
