# Snowflake to BigQuery migration

This document provides an introduction on how you can migrate from Snowflake to BigQuery. The following sections introduce the migration tools to help you perform a BigQuery migration, and outlines some differences between Snowflake and BigQuery to help you plan your migration.

## Migrate workflows from Snowflake to BigQuery

When planning a BigQuery migration, consider the different workflows you have on Snowflake and how you might migrate them individually. For minimal impact on your existing operations, we recommend migrating your SQL queries to BigQuery, and then migrating your schema and code after.

### Migrate SQL queries

To migrate your SQL queries, the BigQuery Migration Service offers various SQL translation features to automate the conversion of your Snowflake SQL queries to GoogleSQL SQL, such as the [batch SQL translator](/bigquery/docs/batch-sql-translator) to translate queries in bulk, the [interactive SQL translator](/bigquery/docs/interactive-sql-translator) to translate individual queries, and the [SQL translation API](/bigquery/docs/api-sql-translator) . These translation services also include Gemini-enhanced functionality to further simplify your SQL query migration process.

As you are translating your SQL queries, carefully review the translated queries to verify that data types and table structures are correctly handled. To do so, we recommend creating a wide range of test cases with different scenarios and data. Then run these test cases on BigQuery to compare the results to the original Snowflake results. If there are any differences, analyze and fix the converted queries.

### Migrate schema and code

**Preview**

This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

To migrate schema and data from Snowflake, use the Snowflake connector in the BigQuery Data Transfer Service to set up a data transfer. When you set up the data transfer, you can specify specific Snowflake tables to include, and also have the connector automatically detect your table schema and data types during a transfer.

For more information about setting up a Snowflake data transfer, see [Schedule a Snowflake transfer](/bigquery/docs/migration/snowflake-transfer) .

#### Incremental transfer

When you make a Snowflake data transfer using the Snowflake connector, you can set up an incremental transfer that only transfers data that was changed since the last data transfer, instead of loading the entire dataset with each data transfer. For more information, see [Schedule a Snowflake transfer](/bigquery/docs/migration/snowflake-transfer) .

## BigQuery security features

When you migrate from Snowflake to BigQuery, consider how Google Cloud handles security differently from Snowflake.

Security in BigQuery is intrinsically linked to [Identity and Access Management (IAM)](/iam/docs/overview) in Google Cloud. IAM privileges define the operations that are permitted on a resource and are enforced at the Google Cloud level, providing a centralized and consistent approach to security management. The following are some key security features of Google Cloud:

  - **Integrated Security** : BigQuery leverages Google Cloud's security features. This includes IAM for granular access control for robust and seamless security integration.
  - **Resource-level security** : IAM focuses on resource-level access control, granting permissions to users and groups for various BigQuery resources and services. This approach allows for effective management of access rights so that users only have the necessary permissions to perform their tasks.
  - **Network security** : BigQuery benefits from Google Cloud's robust network security features, such as [Virtual Private Cloud](/vpc/docs/overview) and [private connections](/vpc/docs/private-service-connect) .

When you migrate from Snowflake to BigQuery, consider the following security-related migration requirements:

  - **IAM Configuration** : You must configure IAM roles and permissions in BigQuery to match your existing Snowflake access control policies. This involves mapping Snowflake roles to appropriate [BigQuery IAM roles and permissions](/bigquery/docs/access-control) .
  - **Fine-grained access control** : If you're using row-level or column-level security in Snowflake, you'll need to implement equivalent controls in BigQuery using [authorized views](/bigquery/docs/authorized-views) or [policy tags](/bigquery/docs/best-practices-policy-tags) .
  - **Views and UDF migration** : When migrating views and UDFs, verify that the associated security controls are properly translated to [authorized views](/bigquery/docs/authorized-views) and [authorized UDFs](/bigquery/docs/user-defined-functions#authorize_routines) in BigQuery.

### Encryption

BigQuery [encrypts](/bigquery/docs/encryption-at-rest) your data at rest and in transit by default. If you require more control over encryption keys, BigQuery supports [customer-managed encryption keys](/bigquery/docs/customer-managed-encryption) in the [Cloud Key Management Service](/kms/docs) . You can also use [column-level encryption](/bigquery/docs/column-key-encrypt) .

To maintain data security during and after migration to BigQuery, consider the following:

  - **Key Management** : If you require customer-managed keys, establish a key management strategy in Cloud Key Management Service and configure BigQuery to use those keys.
  - **Data Masking/Tokenization** : If sensitive data is involved, assess whether data masking or tokenization is required to protect it.
  - **Row-Level Security** : Implement row-level security using authorized views, row-level security filters, or other appropriate methods.
  - **Vulnerability Scanning and Penetration Testing** : Conduct regular vulnerability scanning and penetration testing to check the security posture of your BigQuery environment.

### Roles

Roles are the entities to which privileges on securable objects can be granted and revoked.

In IAM, permissions are grouped into roles. IAM provides three types of roles:

  - **[Basic roles](/bigquery/docs/access-control-primitive-roles) :** These roles include the Owner, Editor, and Viewer roles. You can apply these roles at the project or service resource levels by using the Google Cloud console, the Identity and Access Management API, or the `  gcloud CLI  ` . In general, for the strongest security, we recommend that you use predefined roles to follow the principle of least privilege.
  - **[Predefined roles](/iam/docs/roles-overview#predefined) :** These roles provide more granular access to features in a product (such as BigQuery) and are meant to support common use cases and access control patterns.
  - **[Custom roles](/iam/docs/understanding-custom-roles) :** These roles are composed of user-specified permissions.

### Access control

Snowflake lets you grant roles to other roles, creating a hierarchy of roles. IAM doesn't support a role hierarchy but implements a resource hierarchy. The [IAM hierarchy](/iam/docs/resource-hierarchy-access-control) includes the organization level, folder level, project level, and resource level. You can set IAM roles at any level of the hierarchy, and resources inherit all the policies of their parent resources.

BigQuery supports [table-level access control](/bigquery/docs/table-access-controls-intro) . Table-level permissions determine the users, groups, and service accounts that can access a table or view. You can give a user access to specific tables or views without giving the user access to the complete dataset.

For more granular access, you can also use [column-level access control](/bigquery/docs/column-level-security-intro) or [row-level security](/bigquery/docs/row-level-security-intro) . This type of control provides fine-grained access to sensitive columns by using policy tags or type-based data classifications.

You can also create [authorized views](/bigquery/docs/authorized-views) to limit data access for more fine-grained access control so that specified users can query a view without having read access to the underlying tables.

## Migrate other Snowflake features

Consider the following Snowflake features as you plan your migration to BigQuery. In some cases, you can use other services in Google Cloud to complete your migration.

  - **Time travel:** In BigQuery, you can use [time travel](/bigquery/docs/time-travel) to access data from any point within the last seven days. If you need to access data beyond seven days, consider [exporting regularly scheduled snapshots](/bigquery/docs/scheduling-queries) .

  - **Streams:** BigQuery supports [change data capture (CDC)](https://wikipedia.org/wiki/Change_data_capture) with [Datastream](/datastream/docs) . You can also use CDC software, like [Debezium](https://debezium.io/) , to write records to BigQuery with [Dataflow](/dataflow/docs) . For more information on manually designing a CDC pipeline with BigQuery, see [Migrating data warehouses to BigQuery: Change data capture (CDC)](/bigquery/docs/migration/pipelines#cdc) .

  - **Tasks:** BigQuery lets you schedule queries and streams or stream integration into queries with [Datastream](/datastream/docs) .

  - **External functions:** BigQuery supports external function calls through [Cloud Run functions](/functions/docs/concepts/overview) . You can also use user-defined functions (UDF) like [SQL UDF](/bigquery/docs/user-defined-functions) , although these functions are executed inside of BigQuery.

## Supported data types, properties, and file formats

Snowflake and BigQuery support most of the same data types, though they sometimes use different names. For a complete list of supported data types in Snowflake and BigQuery, see [Data types](/bigquery/docs/migration/snowflake-sql#data-types) . You can also use SQL translation tools, such as the [interactive SQL translator](/bigquery/docs/interactive-sql-translator) , the [SQL translation API](/bigquery/docs/api-sql-translator) , or the [batch SQL translator](/bigquery/docs/batch-sql-translator) , to translate different SQL dialects into GoogleSQL.

For more information about supported data types in BigQuery, see [GoogleSQL data types](/bigquery/docs/reference/standard-sql/data-types) .

Snowflake can export data in the following file formats. You can load the following formats directly into BigQuery:

  - [Loading CSV data from Cloud Storage](/bigquery/docs/loading-data-cloud-storage-csv) .
  - [Loading Parquet data from Cloud Storage](/bigquery/docs/loading-data-cloud-storage-parquet) .
  - [Loading JSON data from Cloud Storage](/bigquery/docs/loading-data-cloud-storage-json) .
  - [Query data from Apache Iceberg](/bigquery/docs/iceberg-tables) .

## Migration tools

The following list describes the tools that you can use to migrate data from Snowflake to BigQuery. For examples of how these tools can be used together in a Snowflake migration pipeline, see [Snowflake migration pipeline examples](/bigquery/docs/migration/snowflake-tutorials#pipeline-examples) .

  - **[`  COPY INTO <location>  ` command](https://docs.snowflake.com/en/sql-reference/sql/copy-into-location.html) :** Use this command in Snowflake to extract data from a Snowflake table directly into a specified Cloud Storage bucket. For an end-to-end example, see [Snowflake to BigQuery (snowflake2bq)](https://github.com/GoogleCloudPlatform/professional-services/tree/master/tools/snowflake2bq) on GitHub.
  - **[Apache Sqoop](https://sqoop.apache.org/) :** To extract data from Snowflake into either HDFS or Cloud Storage, submit Hadoop jobs with the JDBC driver from Sqoop and Snowflake. Sqoop runs in a [Dataproc](/dataproc/docs) environment.
  - **[Snowflake JDBC](https://docs.snowflake.com/en/user-guide/jdbc.html) :** Use this driver with most client tools or applications that support JDBC.

You can use the following generic tools to migrate data from Snowflake to BigQuery:

  - **[The BigQuery Data Transfer Service for Snowflake connector](/bigquery/docs/migration/snowflake-transfer)** ( [Preview](https://cloud.google.com/products#product-launch-stages) ): Perform an automated batch transfer of Cloud Storage data into BigQuery.
  - **The [Google Cloud CLI](/sdk/gcloud/reference/storage) :** Copy downloaded Snowflake files into Cloud Storage with this command-line tool.
  - **[bq command-line tool](/bigquery/docs/bq-command-line-tool) :** Interact with BigQuery using this command-line tool. Common use cases include creating BigQuery table schemas, loading Cloud Storage data into tables, and running queries.
  - **[Cloud Storage client libraries](/storage/docs/reference/libraries) :** Copy downloaded Snowflake files into Cloud Storage with a custom tool that uses the Cloud Storage client libraries.
  - **[BigQuery client libraries](/bigquery/docs/reference/libraries) :** Interact with BigQuery with a custom tool built on top of the BigQuery client library.
  - **[BigQuery query scheduler](/bigquery/docs/scheduling-queries) :** Schedule recurring SQL queries with this built-in BigQuery feature.
  - **[Cloud Composer](/composer/docs) :** Use this fully managed Apache Airflow environment to orchestrate BigQuery load jobs and transformations.

For more information on loading data into BigQuery, see [Loading data into BigQuery](/bigquery/docs/migration/schema-data-overview#loading_the_data_into_bigquery) .

## Pricing

When planning your Snowflake migration, consider the cost of transferring data, storing data, and using services in BigQuery. For more information, see [Pricing](https://cloud.google.com/bigquery/pricing) .

There can be egress costs for moving data out of Snowflake or AWS. There can also be additional costs when transferring data across regions, or transferring data across different cloud providers.

## Get started

The following sections summarize the Snowflake to BigQuery migration process:

### Run a migration assessment

In your Snowflake to BigQuery migration, we recommend that you start by running the [BigQuery migration assessment tool](/bigquery/docs/migration-assessment) to assess the feasibility and potential benefits of moving your data warehouse from Snowflake to BigQuery. This tool provides a structured approach to understanding your current Snowflake environment and estimating the effort involved in a successful migration.

Running the BigQuery migration assessment tool produces an assessment report that contains the following sections:

  - Existing system report: a snapshot of the existing Snowflake system and usage, including the number of databases, schemas, tables, and total size in TB. It also lists the schemas by size and points to potential sub-optimal resource utilization, like tables with no writes or few reads.
  - BigQuery steady state transformation suggestions: shows what the system will look like in BigQuery after the migration. It includes suggestions for optimizing workloads in BigQuery and avoiding wastage.
  - Migration plan: provides information about the migration effort itself. For example, getting from the existing system to the BigQuery steady state. This section includes the count of queries that were automatically translated and the expected time to move each table into BigQuery.

For more information about the results of a migration assessment, see [Review the Looker Studio report](/bigquery/docs/migration-assessment#review_the_data_studio_report) .

### Validate your migration

Once you've migrated your Snowflake data to BigQuery, run the [Data Validation Tool (DVT)](https://github.com/GoogleCloudPlatform/professional-services-data-validator) to perform a data validation on your newly migrated BigQuery data. The DVT validates various functions, from the table level to the row level, to verify that your migrated data works as intended.
