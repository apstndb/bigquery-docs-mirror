# Introduction to BigQuery Migration Service

This document provides an overview of the BigQuery Migration Service.

The BigQuery Migration Service is a comprehensive solution for migrating your data warehouse to BigQuery. It includes features that help you with each phase of migration, including assessment and planning, SQL translation for [a variety of SQL dialects](/bigquery/docs/interactive-sql-translator#supported_sql_dialects) , data transfer, and data validation. Together, these services help you accelerate migrations and reduce risk, shortening the time to value.

The BigQuery Migration Service includes the following features:

  - **BigQuery migration assessment** : Assess and plan your data warehouse migration by running a [BigQuery migration assessment](/bigquery/docs/migration-assessment) .
  - **SQL translation services** : The translation services automate the conversion of your SQL queries into GoogleSQL, including Gemini-enhanced SQL customization. You can use the [batch SQL translator](/bigquery/docs/batch-sql-translator) to migrate your SQL scripts in bulk, or the [interactive SQL translator](/bigquery/docs/interactive-sql-translator) to translate individual queries. You can also use the [SQL translation API](/bigquery/docs/api-sql-translator) to migrate your workloads to BigQuery.
  - **BigQuery Data Transfer Service** : Set up a data transfer that loads data from your data source to BigQuery. For more information, see [What is the BigQuery Data Transfer Service?](/bigquery/docs/dts-introduction) .

You can also use the following open-source tools to help you with your migration process:

  - **Data migration tool** : Use the [data migration tool](https://github.com/GoogleCloudPlatform/data-migration-tool) to automate your data warehouse migration to BigQuery. The tool uses the BigQuery Data Transfer Service, the BigQuery translation services, and the data validation tool to transfer data, translate and validate DDL, DML, and SQL queries.
  - **Data validation tool** : After migrating your data to BigQuery, run the [data validation tool](https://github.com/GoogleCloudPlatform/professional-services-data-validator) to validate that your source and destination tables match.
  - **BigQuery permission mapper** : Use the [permission mapper](https://github.com/GoogleCloudPlatform/professional-services-bigquery-permission-mapper) to automate the creation and maintenance of user-modifiable permission maps. You can use the permission mapper to analyze and reconcile duplicate permissions and user groups, while also generating error reports. The tool outputs JSON and Terraform scripts for BigQuery group, user, and binding creation.
  - **Cloud Composer templates** : Use [Cloud Composer templates](https://github.com/GoogleCloudPlatform/professional-services-composer-templates) to simplify the creation of new Airflow DAGs or the migration of existing orchestrated jobs from on-premise to the cloud.
  - **Cloud Foundation Fabric** : View [Terraform examples and modules for Google Cloud](https://github.com/GoogleCloudPlatform/cloud-foundation-fabric) , including an organization-wide landing zone blueprint, reference blueprints for network patterns and product features, and a library of adaptable modules.

## Quotas

Quotas and limits apply to the number of jobs as well as the size of files. For more information on migration service quotas and limits, see [Quotas and limits](/bigquery/quotas#migration-api-limits) .

## Pricing

There is no charge to use the BigQuery Migration API. However, storage used for input and output files incurs the normal fees. For more information, see [Storage pricing](https://cloud.google.com/bigquery/pricing#storage) .

Additionally, you can use the [cost estimation functionality in Google Cloud Migration Center](/migration-center/docs/migration-center-overview) to generate a cost estimate of running your data warehouse setup that you migrate to BigQuery. For more information, see [Start a cost estimation](/migration-center/docs/estimate/start-estimation) and [Specify data warehousing requirements](/migration-center/docs/estimate/specify-datawarehouse-requirements) .

## What's next

  - For more information on batch SQL translator, see [Batch SQL translator](/bigquery/docs/batch-sql-translator) .
  - For more information on using the interactive SQL translator, see [Interactive SQL translator](/bigquery/docs/interactive-sql-translator) .
  - For more information on BigQuery migration assessment, see [BigQuery migration assessment](/bigquery/docs/migration-assessment) .
  - Learn about the [Data Validation Tool](https://github.com/GoogleCloudPlatform/professional-services-data-validator#data-validation-tool) .
  - For information about quotas and limits for the BigQuery Migration Service, see [Quotas and limits](/bigquery/quotas#migration-api-limits) .
