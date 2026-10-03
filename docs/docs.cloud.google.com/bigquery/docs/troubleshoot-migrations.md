---
name: documents/docs.cloud.google.com/bigquery/docs/troubleshoot-migrations
uri: https://docs.cloud.google.com/bigquery/docs/troubleshoot-migrations
title: Troubleshoot migration issues
description: Troubleshoot common issues when migrating your data warehouse to BigQuery, including migration assessment, SQL translation, and metadata generation errors.
data_source: docs.cloud.google.com
---

# Troubleshoot migration issues

This document helps you troubleshoot common issues when migrating your data warehouse (such as Teradata, Amazon Redshift, Oracle, or Apache Hive) to BigQuery, including issues with migration assessment, interactive and batch SQL translation, and metadata generation using the `dwh-migration-dumper` command-line extraction tool.

To inspect job execution details, error codes, and slot usage for migrated queries and jobs, you can also query the [`INFORMATION_SCHEMA.JOBS` view](https://docs.cloud.google.com/bigquery/docs/information-schema-jobs) .

## Migration assessment

The following sections explain common issues and troubleshooting techniques for migrating your data warehouse to BigQuery.

### `dwh-migration-dumper` tool errors

To troubleshoot errors and warnings in the `dwh-migration-dumper` tool terminal output that occurred during metadata or query logs extraction, see [generate metadata troubleshooting](https://docs.cloud.google.com/bigquery/docs/generate-metadata#troubleshooting) .

### Hive migration errors

The following sections describe common issues that you might encounter when you plan to migrate your data warehouse from Hive to BigQuery.

The `hadoop-migration-assessment` query logs extraction logging hook writes debug log messages in your `hive-server2` logs. If you encounter any issues, review the logging hook debug logs, which contain the `MigrationAssessmentLoggingHook` string.

#### Handle the `ClassNotFoundException` error

This error might be caused by misplacement of the logging hook JAR file. Ensure that you added the JAR file to the `auxlib` folder on the Hive cluster. Alternatively, you can specify the full path to the JAR file in the `hive.aux.jars.path` property—for example, `file:// `` AUXLIB_PATH `` /HiveMigrationAssessmentQueryLogsHooks_deploy.jar` .

#### Subfolders don't appear in the configured folder

This issue might be caused by a misconfiguration or problems during logging hook initialization.

Search your `hive-server2` debug logs for the following logging hook messages:

```
Unable to initialize logger, logging disabled
```

```
Log dir configuration key 'dwhassessment.hook.base-directory' is not set,
logging disabled.
```

```
Error while trying to set permission
```

Review the issue details and see if there is anything that you need to correct to fix the problem.

#### Files don't appear in the folder

This issue might be caused by problems encountered during event processing or while writing to a file.

Search your `hive-server2` debug logs for the following logging hook messages:

```
Failed to close writer for file
```

```
Got exception while processing event
```

```
Error writing record for query
```

Review the issue details and see if there is anything that you need to correct to fix the problem.

#### Some query events are missed

This issue might be caused by a logging hook thread queue overflow.

Search your `hive-server2` debug logs for the following logging hook message:

```
Writer queue is full. Ignoring event
```

If you find this message, consider increasing the `dwhassessment.hook.queue.capacity` parameter.

## Interactive SQL translator

The following sections describe commonly encountered errors when using the interactive SQL translator.

### `RelationNotFound` or `AttributeNotFound` translation issues

After translating a query using the [interactive SQL translator](https://docs.cloud.google.com/bigquery/docs/interactive-sql-translator#translate_a_query_into_standard_sql) , you might encounter a failed translation with the `RelationNotFound` or `AttributeNotFound` error.

You can find failed translations by going to the **Translation details** page in BigQuery in the Google Cloud console and opening the **Log Messages** tab.

To ensure the most accurate translation, you can enter the data definition language (DDL) statements for any tables used in a query prior to the query itself. For example, if you want to translate the Amazon Redshift query `select table1.field1, table2.field1 from table1, table2 where table1.id = table2.id;` , enter the following SQL statements into the interactive SQL translator:

```
create table schema1.table1 (id int, field1 int, field2 varchar(16));
create table schema1.table2 (id int, field1 varchar(30), field2 date);

select table1.field1, table2.field1
from table1, table2
where table1.id = table2.id;
```

#### Fix translation issues with Gemini

> **Preview**
>
> This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

> **Note:** To request feedback or support for this feature, contact <bq-edw-migration-support@google.com> .

To fix failed translation jobs with the `RelationNotFound` or `AttributeNotFound` errors, you can also use Gemini to resolve these issues:

1.  In BigQuery in the Google Cloud console, go to the **Translation details** page and open the **Log Messages** tab.
2.  Click the query that has the message `RelationNotFound` or `AttributeNotFound` in the **Category** column.
3.  Click **Suggested fix** .
4.  Click **Apply** .
5.  To retranslate the query, click **Translate** .

## Batch SQL translator

The following sections describe commonly encountered errors when using the batch SQL translator.

### `RelationNotFound` or `AttributeNotFound` translation issues

After translating a query using the [batch SQL translator](https://docs.cloud.google.com/bigquery/docs/batch-sql-translator#submit_a_translation_job) , you might encounter a failed translation with the `RelationNotFound` or `AttributeNotFound` error.

You can find failed translations by going to the **Translation details** page in BigQuery in the Google Cloud console and opening the **Log Messages** tab.

Translation works best with metadata DDLs. When SQL object definitions can't be found, the translation engine raises `RelationNotFound` or `AttributeNotFound` issues. We recommend using the metadata extractor to generate metadata packages to make sure all object definitions are present. Adding metadata is the recommended first step to resolve most translation errors, because this step often fixes many other errors that are indirectly caused by a lack of metadata.

For more information, see [Generate metadata for translation and assessment](https://docs.cloud.google.com/bigquery/docs/generate-metadata) .

#### Fix translation issues with Gemini

> **Preview**
>
> This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

> **Note:** To request feedback or support for this feature, contact <bq-edw-migration-support@google.com> .

To fix failed translation jobs with the `RelationNotFound` or `AttributeNotFound` errors, you can also use Gemini to resolve these issues:

1.  Go to the **Translation details** page and open the **Log Messages** tab.

2.  Click the query that has the message `RelationNotFound` or `AttributeNotFound` in the **Category** column.

3.  To go to the file and line containing the error in the code tab, click the

    error message.

4.  In the **Action** column, click **Suggested fix** .

5.  Select one of the following options, **Apply** or **Apply and rerun** :

    - To copy the generated schema file from the output directory to the input directory, click **Apply** .
    - To copy the generated schema file from the output directory to the input directory and open a rerun window, click **Apply and rerun** .

## Generate metadata for translation and assessment

The following sections explain some common issues and troubleshooting techniques for the `dwh-migration-dumper` tool.

### Out of memory error

The `java.lang.OutOfMemoryError` error in the `dwh-migration-dumper` tool terminal output is often related to insufficient memory for processing retrieved data. To address this issue, increase available memory or reduce the number of processing threads.

You can increase maximum memory by exporting the `JAVA_OPTS` environment variable:

### Linux

```
export JAVA_OPTS="-Xmx4G"
```

### Windows

```
set JAVA_OPTS="-Xmx4G"
```

You can reduce the number of processing threads (the default is 32) by including the `--thread-pool-size` flag value. This option is supported for `hiveql` and `redshift*` connectors only:

```
dwh-migration-dumper --thread-pool-size=1
```

### Handling a `WARN...Task failed` error

You might sometimes see a `WARN [main] o.c.a.d.MetadataDumper [MetadataDumper.java:107] Task failed: …` error in the `dwh-migration-dumper` tool terminal output. The extraction tool submits multiple queries to the source system, and the output of each query is written to its own file. Seeing this issue indicates that one of these queries failed. However, the failure of one query doesn't prevent the execution of the other queries. If you see more than a couple of `WARN` errors, review the issue details and see if there is anything that you need to correct for the query to run appropriately. For example, if the database user you specified when running the extraction tool lacks permissions to read all metadata, try again with a user with the correct permissions.

### Corrupted ZIP file

To validate the `dwh-migration-dumper` tool ZIP file, download the [`SHA256SUMS.txt` file](https://github.com/google/dwh-migration-tools/releases/latest/download/SHA256SUMS.txt) and run the following command:

### Bash

```
sha256sum --check SHA256SUMS.txt
```

The `OK` result confirms successful checksum verification. Any other message indicates a verification error:

- `FAILED: computed checksum did NOT match` : the ZIP file is corrupted and must be downloaded again.
- `FAILED: listed file could not be read` : the ZIP file version can't be located. Download the checksum and ZIP files from the same release version and place them in the same directory.

### Windows PowerShell

```
(Get-FileHash RELEASE_ZIP_FILENAME).Hash -eq ((Get-Content SHA256SUMS.txt) -Split " ")[0]
```

Replace `RELEASE_ZIP_FILENAME` with the downloaded ZIP filename of the `dwh-migration-dumper` command-line extraction tool release—for example, `dwh-migration-tools-v1.0.52.zip` .

The `True` result confirms successful checksum verification.

The `False` result indicates a verification error. Download the checksum and ZIP files from the same release version and place them in the same directory.

### Teradata query logs extraction is slow

To improve the performance of joining tables that are specified by the `-Dteradata-logs.query-logs-table` and `-Dteradata-logs.sql-logs-table` flags, you can include an additional column of type `DATE` in the `JOIN` condition. This column must be defined in both tables and must be part of the Partitioned Primary Index. To include this column, use the `-Dteradata-logs.log-date-column` flag.

The following example shows how to use the `-Dteradata-logs.log-date-column` flag:

### Bash

```
dwh-migration-dumper \
  -Dteradata-logs.query-logs-table=historicdb.ArchivedQryLogV \
  -Dteradata-logs.sql-logs-table=historicdb.ArchivedDBQLSqlTbl \
  -Dteradata-logs.log-date-column=ArchiveLogDate
```

### Windows PowerShell

```
dwh-migration-dumper `
  "-Dteradata-logs.query-logs-table=historicdb.ArchivedQryLogV" `
  "-Dteradata-logs.sql-logs-table=historicdb.ArchivedDBQLSqlTbl" `
  "-Dteradata-logs.log-date-column=ArchiveLogDate"
```

### Teradata row size limit exceeded

Teradata version 15 has a 64 KB row size limit. If the limit is exceeded, the extraction tool fails with the following message:

```
[Error 9804] [SQLState HY000] Response Row size or Constant Row size overflow
```

To resolve this error, either extend the row limit to 1 MB or split the rows into multiple rows:

- Install and enable the 1 MB Perm and Response Rows feature and current TTU software. For more information, see [Teradata Database Message 9804](https://docs.teradata.com/r/Teradata-VantageCloud-Lake-Analytics-Database-Messages/Database-Messages/9804) .
- Split the long query text into multiple rows by using the `-Dteradata.metadata.max-text-length` and `-Dteradata-logs.max-sql-length` flags.

The following command shows how to use the `-Dteradata.metadata.max-text-length` flag to split long query text into multiple rows of at most 10,000 characters each:

### Bash

```
dwh-migration-dumper \
  --connector teradata \
  -Dteradata.metadata.max-text-length=10000
```

### Windows PowerShell

```
dwh-migration-dumper `
  --connector teradata `
  "-Dteradata.metadata.max-text-length=10000"
```

The following command shows how to use the `-Dteradata-logs.max-sql-length` flag to split long query text into multiple rows of at most 10,000 characters each:

### Bash

```
dwh-migration-dumper \
  --connector teradata-logs \
  -Dteradata-logs.max-sql-length=10000
```

### Windows PowerShell

```
dwh-migration-dumper `
  --connector teradata-logs `
  "-Dteradata-logs.max-sql-length=10000"
```

### Oracle connection issue

In common cases such as an invalid password or hostname, `dwh-migration-dumper` tool prints a meaningful error message describing the root issue. However, in some cases, the error message returned by the Oracle server might be generic and difficult to investigate.

One of these issues is `IO Error: Got minus one from a read call` . This error indicates that the connection to the Oracle server was established, but the server didn't accept the client and closed the connection. This issue typically occurs when the server accepts `TCPS` connections only. By default, `dwh-migration-dumper` tool uses the `TCP` protocol. To solve this issue, you must override the Oracle JDBC connection URL.

Instead of providing the `oracle-service` , `host` , and `port` flags, you can resolve this issue by providing the `url` flag in the following format: `jdbc:oracle:thin:@tcps:// `` HOST_NAME `` : `` PORT `` / `` ORACLE_SERVICE` . Typically, the `TCPS` port number used by the Oracle server is `2484` .

The following example shows how to specify the connection URL in the command:

```
dwh-migration-dumper \
  --connector oracle-stats \
  --url "jdbc:oracle:thin:@tcps://HOST_NAME:PORT/ORACLE_SERVICE" \
  --assessment \
  --driver "JDBC_DRIVER_PATH" \
  --user "USER" \
  --password
```

In addition to changing the connection protocol to `TCPS` , you might need to provide the trustStore SSL configuration that is required to verify the Oracle server certificate. A missing SSL configuration results in an `Unable to find valid certification path` error message. To resolve this issue, set the `JAVA_OPTS` environment variable:

```
set JAVA_OPTS=-Djavax.net.ssl.trustStore="JKS_FILE_LOCATION" -Djavax.net.ssl.trustStoreType=JKS -Djavax.net.ssl.trustStorePassword="PASSWORD"
```

Depending on your Oracle server configuration, you might also need to provide the keyStore configuration. For more information about configuration options, see [SSL With Oracle JDBC Driver](https://www.oracle.com/docs/tech/wp-oracle-jdbc-thin-ssl.pdf) .

## What's next

- Learn more about the [migration overview](https://docs.cloud.google.com/bigquery/docs/migration/migration-overview) .
- Learn how to run a [migration assessment](https://docs.cloud.google.com/bigquery/docs/migration-assessment) .
- Learn how to [translate queries with the interactive SQL translator](https://docs.cloud.google.com/bigquery/docs/interactive-sql-translator) .
- Learn how to [migrate code with the batch SQL translator](https://docs.cloud.google.com/bigquery/docs/batch-sql-translator) .
- Learn how to [generate metadata for translation and assessment](https://docs.cloud.google.com/bigquery/docs/generate-metadata) .
