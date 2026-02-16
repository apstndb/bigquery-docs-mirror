# Generate metadata for translation and assessment

**Preview**

This product is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . Pre-GA products are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

This document describes how to create metadata and query log files by using the `  dwh-migration-dumper  ` command-line extraction tool. The metadata files describe the SQL objects in your source system.

BigQuery Migration Service uses this information to improve the translation of your SQL scripts from your source system dialect to GoogleSQL.

The BigQuery migration assessment uses metadata files and query log files to analyze your existing data warehouse and help assess the effort of moving your data warehouse to BigQuery.

## Overview

You can use the `  dwh-migration-dumper  ` tool to extract metadata information from the database platform that you are migrating to BigQuery. While using the extraction tool isn't required for translation, it is required for BigQuery migration assessment and we strongly recommend using it for all migration tasks.

For more information, see [Create metadata files](/bigquery/docs/batch-sql-translator#create_metadata_files) .

You can use the `  dwh-migration-dumper  ` tool to extract metadata from the following database platforms:

  - Teradata
  - Amazon Redshift
  - Apache Hive
  - Apache Impala
  - Apache Spark
  - Azure Synapse
  - Greenplum
  - SQL Server
  - IBM Netezza
  - Oracle
  - PostgreSQL
  - Snowflake
  - Trino or PrestoSQL
  - Vertica
  - BigQuery

For most of these databases you can also extract query logs.

The `  dwh-migration-dumper  ` tool queries system tables to gather data definition language (DDL) statements related to user and system databases. It does not query the contents of user databases. The tool saves the metadata information from the system tables as CSV files and then zips these files into a single package. You then upload this zip file to Cloud Storage when you upload your source files for translation or assessment.

When using the query logs option, the `  dwh-migration-dumper  ` tool queries system tables for DDL statements and query logs related to user and system databases. These are saved in CSV or yaml format to a subdirectory, and then packed into a zip package. At no point are the contents of user databases queried themselves. At this point, the BigQuery migration assessment requires individual CSV, YAML and text files for query logs so you should unzip all of these files from query logs zip file and upload them for assessment.

The `  dwh-migration-dumper  ` tool can run on Windows, macOS, and Linux.

The `  dwh-migration-dumper  ` tool is available under the [Apache 2 license](https://github.com/google/dwh-migration-tools/blob/main/LICENSE) .

If you choose not to use the `  dwh-migration-dumper  ` tool for translation, you can manually provide metadata files by collecting the data definition language (DDL) statements for the SQL objects in your source system into separate text files.

Providing metadata and query logs extracted with the tool is required for migration assessment using BigQuery migration assessment.

## Compliance requirements

We provide the compiled `  dwh-migration-dumper  ` tool binary for ease of use. If you need to audit the tool to ensure that it meets compliance requirements, you can review the source code from the [`  dwh-migration-dumper  ` tool GitHub repository](https://github.com/google/dwh-migration-tools/tree/main/dumper) , and compile your own binary.

## Prerequisites

### Install Java

The server on which you plan to run `  dwh-migration-dumper  ` tool must have Java 8 or higher installed. If it doesn't, download Java from the [Java downloads page](https://www.java.com/download/) and install it.

### Required permissions

The user account that you specify for connecting the `  dwh-migration-dumper  ` tool to the source system must have permissions to read metadata from that system. Confirm that this account has appropriate role membership to query the metadata resources available for your platform. For example, `  INFORMATION_SCHEMA  ` is a metadata resource that is common across several platforms.

## Install the `     dwh-migration-dumper    ` tool

To install the `  dwh-migration-dumper  ` tool, follow these steps:

1.  On the machine where you want to run the `  dwh-migration-dumper  ` tool, download the zip file from the [`  dwh-migration-dumper  ` tool GitHub repository](https://github.com/google/dwh-migration-tools/releases/latest) .

2.  To validate the `  dwh-migration-dumper  ` tool zip file, download the [`  SHA256SUMS.txt  ` file](https://github.com/google/dwh-migration-tools/releases/latest/download/SHA256SUMS.txt) and run the following command:
    
    ### Bash
    
    ``` text
    sha256sum --check SHA256SUMS.txt
    ```
    
    If verification fails, see [Troubleshooting](#corrupted_zip_file) .
    
    ### Windows PowerShell
    
    ``` text
    (Get-FileHash RELEASE_ZIP_FILENAME).Hash -eq ((Get-Content SHA256SUMS.txt) -Split " ")[0]
    ```
    
    Replace the `  RELEASE_ZIP_FILENAME  ` with the downloaded zip filename of the `  dwh-migration-dumper  ` command-line extraction tool release—for example, `  dwh-migration-tools-v1.0.52.zip  `
    
    The `  True  ` result confirms successful checksum verification.
    
    The `  False  ` result indicates verification error. Make sure the checksum and zip files are downloaded from the same release version and placed in the same directory.

3.  Extract the zip file. The extraction tool binary is in the `  /bin  ` subdirectory of the folder created by extracting the zip file.

4.  Update the `  PATH  ` environment variable to include the installation path for the extraction tool.

## Run the `     dwh-migration-dumper    ` tool

The `  dwh-migration-dumper  ` tool uses the following format:

``` text
dwh-migration-dumper [FLAGS]
```

Running the `  dwh-migration-dumper  ` tool creates an output file named `  dwh-migration-<source platform>-metadata.zip  ` —for example, `  dwh-migration-teradata-metadata.zip  ` , in your working directory.

**Tip:** When using Windows PowerShell, surround flags with double quotes—for example, `  dwh-migration-dumper "-Dteradata-logs.utility-logs-table=historicdb.ArchivedUtilityLogs"  ` .

Use the following instructions to learn how to run the `  dwh-migration-dumper  ` tool for your source platform.

### Teradata

To allow the `  dwh-migration-dumper  ` tool to connect to Teradata, download their JDBC driver from Teradata's [download page](https://downloads.teradata.com/download/connectivity/jdbc-driver) .

The following table describes the commonly used flags for extracting Teradata metadata and query logs by using the extraction tool. For information about all supported flags, see [global flags](#global_flags) .

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Name</strong></th>
<th><strong>Default value</strong></th>
<th><strong>Description</strong></th>
<th><strong>Required</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">         --assessment        </code></td>
<td></td>
<td><p>Turns on assessment mode when generating database logs or extracting metadata. The <code dir="ltr" translate="no">          dwh-migration-dumper         </code> tool generates required metadata statistics for BigQuery migration assessment when used for metadata extraction. When used for query logs it extracts additional columns for BigQuery migration assessment.</p></td>
<td>Required when using for running assessment, not required for translation.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         --connector        </code></td>
<td></td>
<td>The name of the connector to use, in this case <strong>teradata</strong> for metadata or <strong>teradata-logs</strong> for query logs.</td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         --database        </code></td>
<td></td>
<td><p>A list of the databases to extract, separated by commas. The database names might be case-sensitive, depending on the Teradata server configuration.</p>
<p>If this flag is used in combination with the <code dir="ltr" translate="no">          teradata         </code> connector, then the <code dir="ltr" translate="no">          dwh-migration-dumper         </code> tool filters the metadata tables and views by the provided list of databases. The exceptions are the <code dir="ltr" translate="no">          DatabasesV         </code> and <code dir="ltr" translate="no">          RoleMembersV         </code> views - the <code dir="ltr" translate="no">          dwh-migration-dumper         </code> tool extracts the databases and users from these views without filtering by the database name.</p>
<p>This flag cannot be used in combination with the <code dir="ltr" translate="no">          teradata-logs         </code> connector. Query logs are always extracted for all the databases.</p></td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         --driver        </code></td>
<td></td>
<td>The absolute or relative path to the driver JAR file to use for this connection. You can specify multiple driver JAR files, separating them by commas.</td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         --host        </code></td>
<td>localhost</td>
<td>The hostname or IP address of the database server.</td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         --password        </code></td>
<td></td>
<td>The password to use for the database connection.</td>
<td>If not specified, the extraction tool uses a secure prompt to request it.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         --port        </code></td>
<td>1025</td>
<td>The port of the database server.</td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         --user        </code></td>
<td></td>
<td><p>The username to use for the database connection.</p></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         --query-log-alternates        </code></td>
<td></td>
<td><p>For the <code dir="ltr" translate="no">          teradata-logs         </code> connector only.</p>
<p>To extract the query logs from an alternative location, we recommend that you use the <code dir="ltr" translate="no">          -Dteradata-logs.query-logs-table         </code> and <code dir="ltr" translate="no">          -Dteradata-logs.sql-logs-table         </code> flags instead.</p>
<p>By default, the query logs are extracted from the tables <code dir="ltr" translate="no">          dbc.DBQLogTbl         </code> and <code dir="ltr" translate="no">          dbc.DBQLSQLTbl         </code> . If you use the <code dir="ltr" translate="no">          --assessment         </code> flag, then the query logs are extracted from the view <code dir="ltr" translate="no">          dbc.QryLogV         </code> and from the table <code dir="ltr" translate="no">          dbc.DBQLSQLTbl         </code> . If you need to extract the query logs from an alternative location, you can specify the fully-qualified names of the tables or views by using the <code dir="ltr" translate="no">          --query-log-alternates         </code> flag. The first parameter references the alternative to the <code dir="ltr" translate="no">          dbc.DBQLogTbl         </code> table, and the second parameter references the alternative to the <code dir="ltr" translate="no">          dbc.DBQLSQLTbl         </code> table. Both parameters are required.<br />
The <code dir="ltr" translate="no">          -Dteradata-logs.log-date-column         </code> flag can be used to improve extraction performance when both tables have an indexed column of type <code dir="ltr" translate="no">          DATE         </code> .</p>
<p>Example: <code dir="ltr" translate="no">          --query-log-alternates historicdb.ArchivedQryLogV,historicdb.ArchivedDBQLSqlTbl         </code></p></td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         -Dteradata.tmode        </code></td>
<td></td>
<td><p>The transaction mode for the connection. The following values are supported:</p>
<ul>
<li><code dir="ltr" translate="no">           ANSI          </code> : ANSI mode. This is the default mode (if the flag is not specified)</li>
<li><code dir="ltr" translate="no">           TERA          </code> : Teradata transaction mode (BTET)</li>
<li><code dir="ltr" translate="no">           DEFAULT          </code> : use the default transaction mode configured on the database server</li>
<li><code dir="ltr" translate="no">           NONE          </code> : no mode is set for the connection</li>
</ul>
<p>Example (Bash):<br />
<code dir="ltr" translate="no">          -Dteradata.tmode=TERA         </code></p>
<p>Example (Windows PowerShell):<br />
<code dir="ltr" translate="no">          "-Dteradata.tmode=TERA"         </code></p></td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         -Dteradata-logs.log-date-column        </code></td>
<td></td>
<td><p>For the <code dir="ltr" translate="no">          teradata-logs         </code> connector only.</p>
<p>To improve performance of joining tables that are specified by the <code dir="ltr" translate="no">          -Dteradata-logs.query-logs-table         </code> and <code dir="ltr" translate="no">          -Dteradata-logs.sql-logs-table         </code> flags, you can include an additional column of type <code dir="ltr" translate="no">          DATE         </code> in the <code dir="ltr" translate="no">          JOIN         </code> condition. This column must be defined in both tables and it must be part of the Partitioned Primary Index.</p>
<p>Example (Bash):<br />
<code dir="ltr" translate="no">          -Dteradata-logs.log-date-column=ArchiveLogDate         </code></p>
<p>Example (Windows PowerShell):<br />
<code dir="ltr" translate="no">          "-Dteradata-logs.log-date-column=ArchiveLogDate"         </code></p></td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         -Dteradata-logs.query-logs-table        </code></td>
<td></td>
<td><p>For the <code dir="ltr" translate="no">          teradata-logs         </code> connector only.</p>
<p>By default, the query logs are extracted from the <code dir="ltr" translate="no">          dbc.DBQLogTbl         </code> table. If you use the <code dir="ltr" translate="no">          --assessment         </code> flag, then the query logs are extracted from the view <code dir="ltr" translate="no">          dbc.QryLogV         </code> . If you need to extract the query logs from an alternative location, you can specify the fully-qualified name of the table or view by using this flag.<br />
See <code dir="ltr" translate="no">          -Dteradata-logs.log-date-column         </code> flag to improve extraction performance.</p>
<p>Example (Bash):<br />
<code dir="ltr" translate="no">          -Dteradata-logs.query-logs-table=historicdb.ArchivedQryLogV         </code></p>
<p>Example (Windows PowerShell):<br />
<code dir="ltr" translate="no">          "-Dteradata-logs.query-logs-table=historicdb.ArchivedQryLogV"         </code></p></td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         -Dteradata-logs.sql-logs-table        </code></td>
<td></td>
<td><p>For the <code dir="ltr" translate="no">          teradata-logs         </code> connector only.</p>
<p>By default, the query logs containing SQL text are extracted from the <code dir="ltr" translate="no">          dbc.DBQLSqlTbl         </code> table. If you need to extract them from an alternative location, you can specify the fully-qualified name of the table or view by using this flag.<br />
See <code dir="ltr" translate="no">          -Dteradata-logs.log-date-column         </code> flag to improve extraction performance.</p>
<p>Example (Bash):<br />
<code dir="ltr" translate="no">          -Dteradata-logs.sql-logs-table=historicdb.ArchivedDBQLSqlTbl         </code></p>
<p>Example (Windows PowerShell):<br />
<code dir="ltr" translate="no">          "-Dteradata-logs.sql-logs-table=historicdb.ArchivedDBQLSqlTbl"         </code></p></td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         -Dteradata-logs.utility-logs-table        </code></td>
<td></td>
<td><p>For the <code dir="ltr" translate="no">          teradata-logs         </code> connector only.</p>
<p>By default, the utility logs are extracted from the table <code dir="ltr" translate="no">          dbc.DBQLUtilityTbl         </code> . If you need to extract the utility logs from an alternative location, you can specify the fully-qualified name of the table by using the <code dir="ltr" translate="no">          -Dteradata-logs.utility-logs-table         </code> flag.</p>
<p>Example (Bash):<br />
<code dir="ltr" translate="no">          -Dteradata-logs.utility-logs-table=historicdb.ArchivedUtilityLogs         </code></p>
<p>Example (Windows PowerShell):<br />
<code dir="ltr" translate="no">          "-Dteradata-logs.utility-logs-table=historicdb.ArchivedUtilityLogs"         </code></p></td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         -Dteradata-logs.res-usage-scpu-table        </code></td>
<td></td>
<td><p>For the <code dir="ltr" translate="no">          teradata-logs         </code> connector only.</p>
<p>By default, the SCPU resource usage logs are extracted from the table <code dir="ltr" translate="no">          dbc.ResUsageScpu         </code> . If you need to extract these from an alternative location, you can specify the fully-qualified name of the table by using the <code dir="ltr" translate="no">          -Dteradata-logs.res-usage-scpu-table         </code> flag.</p>
<p>Example (Bash):<br />
<code dir="ltr" translate="no">          -Dteradata-logs.res-usage-scpu-table=historicdb.ArchivedResUsageScpu         </code></p>
<p>Example (Windows PowerShell):<br />
<code dir="ltr" translate="no">          "-Dteradata-logs.res-usage-scpu-table=historicdb.ArchivedResUsageScpu"         </code></p></td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         -Dteradata-logs.res-usage-spma-table        </code></td>
<td></td>
<td><p>For the <code dir="ltr" translate="no">          teradata-logs         </code> connector only.</p>
<p>By default, the SPMA resource usage logs are extracted from the table <code dir="ltr" translate="no">          dbc.ResUsageSpma         </code> . If you need to extract these logs from an alternative location, you can specify the fully-qualified name of the table by using the <code dir="ltr" translate="no">          -Dteradata-logs.res-usage-spma-table         </code> flag.</p>
<p>Example (Bash):<br />
<code dir="ltr" translate="no">          -Dteradata-logs.res-usage-spma-table=historicdb.ArchivedResUsageSpma         </code></p>
<p>Example (Windows PowerShell):<br />
<code dir="ltr" translate="no">          "-Dteradata-logs.res-usage-spma-table=historicdb.ArchivedResUsageSpma"         </code></p></td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         --query-log-start        </code></td>
<td></td>
<td><p>The start time (inclusive) for query logs to extract. The value is truncated to the hour. This flag is only available for the <strong>teradata-logs</strong> connector.</p>
<p>Example: <code dir="ltr" translate="no">          --query-log-start "2023-01-01 14:00:00"         </code></p></td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         --query-log-end        </code></td>
<td></td>
<td><p>The end time (exclusive) for query logs to extract. The value is truncated to the hour. This flag is only available for the <strong>teradata-logs</strong> connector.</p>
<p>Example: <code dir="ltr" translate="no">          --query-log-end "2023-01-15 22:00:00"         </code></p></td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         -Dteradata.metadata.tablesizev.max-rows        </code></td>
<td></td>
<td><p>For the <code dir="ltr" translate="no">          teradata         </code> connector only.</p>
<p>Limit the number of rows extracted from the view <code dir="ltr" translate="no">          TableSizeV         </code> . The rows are grouped by the columns <code dir="ltr" translate="no">          DatabaseName         </code> , <code dir="ltr" translate="no">          AccountName         </code> , and <code dir="ltr" translate="no">          TableName         </code> , and then sorted in descending order by the size of the permanent space (the expression <code dir="ltr" translate="no">          SUM(CurrentPerm)         </code> ). Then, the specified number of rows are extracted.</p>
<p>Example (Bash):<br />
<code dir="ltr" translate="no">          -Dteradata.metadata.tablesizev.max-rows=100000         </code></p>
<p>Example (Windows PowerShell):<br />
<code dir="ltr" translate="no">          "-Dteradata.metadata.tablesizev.max-rows=100000"         </code></p></td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         -Dteradata.metadata.diskspacev.max-rows        </code></td>
<td></td>
<td><p>For the <code dir="ltr" translate="no">          teradata         </code> connector only.</p>
<p>Limit the number of rows extracted from the view <code dir="ltr" translate="no">          DiskSpaceV         </code> . The rows are sorted in descending order by the size of the permanent space (column <code dir="ltr" translate="no">          CurrentPerm         </code> ), and then the specified number of rows are extracted.</p>
<p>Example (Bash):<br />
<code dir="ltr" translate="no">          -Dteradata.metadata.diskspacev.max-rows=100000         </code></p>
<p>Example (Windows PowerShell):<br />
<code dir="ltr" translate="no">          "-Dteradata.metadata.diskspacev.max-rows=100000"         </code></p></td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         -Dteradata.metadata.databasesv.users.max-rows        </code></td>
<td></td>
<td><p>For the <code dir="ltr" translate="no">          teradata         </code> connector only.</p>
<p>Limit the number of rows that represent users ( <code dir="ltr" translate="no">          DBKind='U'         </code> ) that are extracted from the view <code dir="ltr" translate="no">          DatabasesV         </code> . The rows are sorted in descending order by the column <code dir="ltr" translate="no">          PermSpace         </code> , and then the specified number of rows are extracted.</p>
<p>Example (Bash):<br />
<code dir="ltr" translate="no">          -Dteradata.metadata.databasesv.users.max-rows=100000         </code></p>
<p>Example (Windows PowerShell):<br />
<code dir="ltr" translate="no">          "-Dteradata.metadata.databasesv.users.max-rows=100000"         </code></p></td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         -Dteradata.metadata.databasesv.dbs.max-rows        </code></td>
<td></td>
<td><p>For the <code dir="ltr" translate="no">          teradata         </code> connector only.</p>
<p>Limit the number of rows that represent databases ( <code dir="ltr" translate="no">          DBKind='D'         </code> ) that are extracted from the view <code dir="ltr" translate="no">          DatabasesV         </code> . The rows are sorted in descending order by the column <code dir="ltr" translate="no">          PermSpace         </code> , and then the specified number of rows are extracted.</p>
<p>Example (Bash):<br />
<code dir="ltr" translate="no">          -Dteradata.metadata.databasesv.dbs.max-rows=100000         </code></p>
<p>Example (Windows PowerShell):<br />
<code dir="ltr" translate="no">          "-Dteradata.metadata.databasesv.dbs.max-rows=100000"         </code></p></td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         -Dteradata.metadata.max-text-length        </code></td>
<td></td>
<td><p>For the <code dir="ltr" translate="no">          teradata         </code> connector only.</p>
<p>Maximum length of the text column when extracting the data from the <code dir="ltr" translate="no">          TableTextV         </code> view. Text longer than the defined limit will be split into multiple rows. Allowed range: between 5000 and 32000 (inclusive).</p>
<p>Example (Bash):<br />
<code dir="ltr" translate="no">          -Dteradata.metadata.max-text-length=10000         </code></p>
<p>Example (Windows PowerShell):<br />
<code dir="ltr" translate="no">          "-Dteradata.metadata.max-text-length=10000"         </code></p></td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         -Dteradata-logs.max-sql-length        </code></td>
<td></td>
<td><p>For the <code dir="ltr" translate="no">          teradata-logs         </code> connector only.</p>
<p>Maximum length of the <code dir="ltr" translate="no">          DBQLSqlTbl.SqlTextInfo         </code> column. Query text longer than the defined limit will be split into multiple rows. Allowed range: between 5000 and 31000 (inclusive).</p>
<p>Example (Bash):<br />
<code dir="ltr" translate="no">          -Dteradata-logs.max-sql-length=10000         </code></p>
<p>Example (Windows PowerShell):<br />
<code dir="ltr" translate="no">          "-Dteradata-logs.max-sql-length=10000"         </code></p></td>
<td>No</td>
</tr>
</tbody>
</table>

#### Examples

The following example shows how to extract metadata for two Teradata databases on the local host:

``` text
dwh-migration-dumper \
  --connector teradata \
  --user user \
  --password password \
  --database database1,database2 \
  --driver path/terajdbc4.jar
```

The following example shows how to extract query logs for Assessment on the local host for authentication:

``` text
dwh-migration-dumper \
  --connector teradata-logs \
  --assessment \
  --user user \
  --password password \
  --driver path/terajdbc4.jar
```

#### Tables and views extracted by the `       dwh-migration-dumper      ` tool

The following tables and views are extracted when you use the `  teradata  ` connector:

  - `  DBC.ColumnsV  `
  - `  DBC.DatabasesV  `
  - `  DBC.DBCInfo  `
  - `  DBC.FunctionsV  `
  - `  DBC.IndicesV  `
  - `  DBC.PartitioningConstraintsV  `
  - `  DBC.TablesV  `
  - `  DBC.TableTextV  `

The following additional tables and views are extracted when you use the `  teradata  ` connector with `  --assessment  ` flag:

  - `  DBC.All_RI_ChildrenV  `
  - `  DBC.All_RI_ParentsV  `
  - `  DBC.AllTempTablesVX  `
  - `  DBC.DiskSpaceV  `
  - `  DBC.RoleMembersV  `
  - `  DBC.StatsV  `
  - `  DBC.TableSizeV  `

The following tables and views are extracted when you use the `  teradata-logs  ` connector:

  - `  DBC.DBQLogTbl  ` (changes to `  DBC.QryLogV  ` if `  --assessment  ` flag is used)
  - `  DBC.DBQLSqlTbl  `

The following additional tables and views are extracted when you use the `  teradata-logs  ` connector with `  --assessment  ` flag:

  - `  DBC.DBQLUtilityTbl  `
  - `  DBC.ResUsageScpu  `
  - `  DBC.ResUsageSpma  `

### Redshift

You can use any of the following Amazon Redshift authentication and authorization mechanisms with the extraction tool:

  - A username and password.
  - An AWS Identity and Access Management (Identity and Access Management (IAM)) access key ID and secret key.
  - An AWS IAM profile name.

To authenticate with the username and password, use the Amazon Redshift default PostgreSQL JDBC driver. To authenticate with AWS IAM, use the Amazon Redshift JDBC driver, which you can download from their [download page](https://docs.aws.amazon.com/redshift/latest/mgmt/jdbc20-download-driver.html) .

The following table describes the commonly used flags for extracting Amazon Redshift metadata and query logs by using the `  dwh-migration-dumper  ` tool. For information about all supported flags, see [global flags](#global_flags) .

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Name</strong></th>
<th><strong>Default value</strong></th>
<th><strong>Description</strong></th>
<th><strong>Required</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">         --assessment        </code></td>
<td></td>
<td><p>Turning on assessment mode when generating database logs or extracting metadata. It generates required metadata statistics for BigQuery migration assessment when used for metadata extraction. When used for query logs extraction it generates query metrics statistics for BigQuery migration assessment.</p></td>
<td>Required when running in assessment mode, not required for translation.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         --connector        </code></td>
<td></td>
<td>The name of the connector to use, in this case <strong>redshift</strong> for metadata or <strong>redshift-raw-logs</strong> for query logs.</td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         --database        </code></td>
<td>If not specified, Amazon Redshift uses the <code dir="ltr" translate="no">         --user        </code> value as the default database name.</td>
<td><p>The name of the database to connect to.</p></td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         --driver        </code></td>
<td>If not specified, Amazon Redshift uses the default PostgreSQL JDBC driver.</td>
<td>The absolute or relative path to the driver JAR file to use for this connection. You can specify multiple driver JAR files, separating them by commas.</td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         --host        </code></td>
<td>localhost</td>
<td>The hostname or IP address of the database server.</td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         --iam-accesskeyid        </code></td>
<td></td>
<td><p>The AWS IAM access key ID to use for authentication. The access key is a string of characters, something like <code dir="ltr" translate="no">          AKIAIOSFODNN7EXAMPLE         </code> .</p>
<p>Use in conjunction with the <code dir="ltr" translate="no">          --iam-secretaccesskey         </code> flag. Do not use this flag when specifying the <code dir="ltr" translate="no">          --iam-profile         </code> or <code dir="ltr" translate="no">          --password         </code> flags.</p></td>
<td><p>Not explicitly, but you must provide authentication information through one of the following methods:</p>
<ul>
<li>Using this flag in conjunction with the <code dir="ltr" translate="no">           --iam-secretaccesskey          </code> flag.</li>
<li>Using the <code dir="ltr" translate="no">           --iam-profile          </code> flag.</li>
<li>Using the <code dir="ltr" translate="no">           --password          </code> flag in conjunction with the <code dir="ltr" translate="no">           --user          </code> flag.</li>
</ul></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         --iam-profile        </code></td>
<td></td>
<td><p>The AWS IAM profile to use for authentication. You can retrieve a profile value to use by examining the <code dir="ltr" translate="no">          $HOME/.aws/credentials         </code> file or by running <code dir="ltr" translate="no">          aws configure list-profiles         </code> .</p>
<p>Do not use this flag with the <code dir="ltr" translate="no">          --iam-accesskeyid         </code> , <code dir="ltr" translate="no">          --iam-secretaccesskey         </code> or <code dir="ltr" translate="no">          --password         </code> flags.</p></td>
<td><p>Not explicitly, but you must provide authentication information through one of the following methods:</p>
<ul>
<li>Using this flag.</li>
<li>Using the <code dir="ltr" translate="no">           --iam-accesskeyid          </code> flag in conjunction with the <code dir="ltr" translate="no">           --iam-secretaccesskey          </code> flag.</li>
<li>Using the <code dir="ltr" translate="no">           --password          </code> flag in conjunction with the <code dir="ltr" translate="no">           --user          </code> flag.</li>
</ul></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         --iam-secretaccesskey        </code></td>
<td></td>
<td><p>The AWS IAM secret access key to use for authentication. The secret access key is a string of characters, something like <code dir="ltr" translate="no">          wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY         </code> .</p>
<p>Use in conjunction with the <code dir="ltr" translate="no">          --iam-accesskeyid         </code> flag. Do not use this flag with the <code dir="ltr" translate="no">          --iam-profile         </code> or <code dir="ltr" translate="no">          --password         </code> flags.</p></td>
<td><p>Not explicitly, but you must provide authentication information through one of the following methods:</p>
<ul>
<li>Using this flag in conjunction with the <code dir="ltr" translate="no">           --iam-accesskeyid          </code> flag.</li>
<li>Using the <code dir="ltr" translate="no">           --iam-profile          </code> flag.</li>
<li>Using the <code dir="ltr" translate="no">           --password          </code> flag in conjunction with the <code dir="ltr" translate="no">           --user          </code> flag.</li>
</ul></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         --password        </code></td>
<td></td>
<td>The password to use for the database connection.
<p>Do not use this flag with the <code dir="ltr" translate="no">          --iam-accesskeyid         </code> , <code dir="ltr" translate="no">          --iam-secretaccesskey         </code> or <code dir="ltr" translate="no">          --iam-profile         </code> flags.</p></td>
<td><p>Not explicitly, but you must provide authentication information through one of the following methods:</p>
<ul>
<li>Using this flag in conjunction with the <code dir="ltr" translate="no">           --user          </code> flag.</li>
<li>Using the <code dir="ltr" translate="no">           --iam-accesskeyid          </code> flag in conjunction with the <code dir="ltr" translate="no">           --iam-secretaccesskey          </code> flag.</li>
<li>Using the <code dir="ltr" translate="no">           --password          </code> flag.</li>
</ul></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         --port        </code></td>
<td>5439</td>
<td>The port of the database server.</td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         --user        </code></td>
<td></td>
<td>The username to use for the database connection.</td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         --query-log-start        </code></td>
<td></td>
<td><p>The start time (inclusive) for query logs to extract. The value is truncated to the hour. This flag is only available for the <strong>redshift-raw-logs</strong> connector.</p>
<p>Example: <code dir="ltr" translate="no">          --query-log-start "2023-01-01 14:00:00"         </code></p></td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         --query-log-end        </code></td>
<td></td>
<td><p>The end time (exclusive) for query logs to extract. The value is truncated to the hour. This flag is only available for the <strong>redshift-raw-logs</strong> connector.</p>
<p>Example: <code dir="ltr" translate="no">          --query-log-end "2023-01-15 22:00:00"         </code></p></td>
<td>No</td>
</tr>
</tbody>
</table>

#### Examples

The following example shows how to extract metadata from an Amazon Redshift database on a specified host, using AWS IAM keys for authentication:

``` text
dwh-migration-dumper \
  --connector redshift \
  --database database \
  --driver path/redshift-jdbc42-version.jar \
  --host host.region.redshift.amazonaws.com \
  --iam-accesskeyid access_key_ID \
  --iam-secretaccesskey secret_access-key \
  --user user
```

The following example shows how to extract metadata from an Amazon Redshift database on the default host, using the username and password for authentication:

``` text
dwh-migration-dumper \
  --connector redshift \
  --database database \
  --password password \
  --user user
```

The following example shows how to extract metadata from an Amazon Redshift database on a specified host, using an AWS IAM profile for authentication:

``` text
dwh-migration-dumper \
  --connector redshift \
  --database database \
  --driver path/redshift-jdbc42-version.jar \
  --host host.region.redshift.amazonaws.com \
  --iam-profile profile \
  --user user \
  --assessment
```

The following example shows how to extract query logs for Assessment from an Amazon Redshift database on a specified host, using an AWS IAM profile for authentication:

``` text
dwh-migration-dumper \
  --connector redshift-raw-logs \
  --database database \
  --driver path/redshift-jdbc42-version.jar \
  --host 123.456.789.012 \
  --iam-profile profile \
  --user user \
  --assessment
```

#### Tables and views extracted by the `       dwh-migration-dumper      ` tool

The following tables and views are extracted when you use the `  redshift  ` connector:

  - `  SVV_COLUMNS  `
  - `  SVV_EXTERNAL_COLUMNS  `
  - `  SVV_EXTERNAL_DATABASES  `
  - `  SVV_EXTERNAL_PARTITIONS  `
  - `  SVV_EXTERNAL_SCHEMAS  `
  - `  SVV_EXTERNAL_TABLES  `
  - `  SVV_TABLES  `
  - `  SVV_TABLE_INFO  `
  - `  INFORMATION_SCHEMA.COLUMNS  `
  - `  PG_CAST  `
  - `  PG_DATABASE  `
  - `  PG_LANGUAGE  `
  - `  PG_LIBRARY  `
  - `  PG_NAMESPACE  `
  - `  PG_OPERATOR  `
  - `  PG_PROC  `
  - `  PG_TABLE_DEF  `
  - `  PG_TABLES  `
  - `  PG_TYPE  `
  - `  PG_VIEWS  `

The following additional tables and views are extracted when you use the `  redshift  ` connector with `  --assessment  ` flag:

  - `  SVV_DISKUSAGE  `
  - `  STV_MV_INFO  `
  - `  STV_WLM_SERVICE_CLASS_CONFIG  `
  - `  STV_WLM_SERVICE_CLASS_STATE  `

The following tables and views are extracted when you use the `  redshift-raw-logs  ` connector:

  - `  STL_DDLTEXT  `
  - `  STL_QUERY  `
  - `  STL_QUERYTEXT  `
  - `  PG_USER  `

The following additional tables and views are extracted when you use the `  redshift-raw-logs  ` connector with `  --assessment  ` flag:

  - `  STL_QUERY_METRICS  `
  - `  SVL_QUERY_QUEUE_INFO  `
  - `  STL_WLM_QUERY  `

For information about the system views and tables in Redshift, see [Redshift system views](https://docs.aws.amazon.com/redshift/latest/dg/c_intro_system_views.html) and [Redshift system catalog tables](https://docs.aws.amazon.com/redshift/latest/dg/c_intro_catalog_views.html) .

### Hive/Impala/Spark or Trino/PrestoSQL

The `  dwh-migration-dumper  ` tool only supports authentication to Apache Hive metastore through Kerberos. So the `  --user  ` and `  --password  ` flags aren't used, instead use the `  --hive-kerberos-url  ` flag to supply the Kerberos authentication details.

The following table describes the commonly used flags for extracting Apache Hive, Impala, Spark, Presto, or Trino metadata by using the extraction tool. For information about all supported flags, see [global flags](#global_flags) .

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Name</strong></th>
<th><strong>Default value</strong></th>
<th><strong>Description</strong></th>
<th><strong>Required</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">         --assessment        </code></td>
<td></td>
<td><p>Turns on assessment mode when extracting metadata. The <code dir="ltr" translate="no">          dwh-migration-dumper         </code> tool generates required metadata statistics for BigQuery migration assessment when used for metadata extraction.</p></td>
<td>Required for assessment. Not required for translation.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         --connector        </code></td>
<td></td>
<td>The name of the connector to use, in this case <strong>hiveql</strong> .</td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         --hive-metastore-dump-partition-metadata        </code></td>
<td>true</td>
<td><p>Causes the <code dir="ltr" translate="no">          dwh-migration-dumper         </code> tool to extract partition metadata. You might want to set this flag to <code dir="ltr" translate="no">          false         </code> for production metastore with a significant number of partitions, due to Thrift client performance implications. This improves the extraction tool performance, but causes some loss of partition optimization on the BigQuery side.</p>
<p>Don't use this flag with the <code dir="ltr" translate="no">          --assessment         </code> flag, as it will have no effect.</p></td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         --hive-metastore-version        </code></td>
<td>2.3.6</td>
<td><p>When you run the <code dir="ltr" translate="no">          dwh-migration-dumper         </code> tool, it selects the appropriate <a href="https://thrift.apache.org/">Thrift</a> specification to use for communicating with your Apache Hive server, based on the value of this flag. If the extraction tool doesn't have an appropriate Thrift specification, it uses the 2.3.6 client and emits a warning to <code dir="ltr" translate="no">          stdout         </code> . If this occurs, please <a href="https://cloud.google.com/support-hub">contact Support</a> and provide the Apache Hive version number you requested.</p></td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         --host        </code></td>
<td>localhost</td>
<td>The hostname or IP address of the database server.</td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         --port        </code></td>
<td>9083</td>
<td>The port of the database server.</td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         --hive-kerberos-url        </code></td>
<td></td>
<td>The Kerberos principal and host to use for authentication.</td>
<td>Required for clusters with enabled Kerberos authentication.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         -Dhiveql.rpc.protection        </code></td>
<td></td>
<td><p>The RPC protection configuration level. This determines the Quality of Protection (QOP) of the Simple Authentication and Security Layer (SASL) connection between cluster and the <code dir="ltr" translate="no">          dwh-migration-dumper         </code> tool.</p>
<p>Must be equal to the value of the <code dir="ltr" translate="no">          hadoop.rpc.protection         </code> parameter inside the <code dir="ltr" translate="no">          /etc/hadoop/conf/core-site.xml         </code> file on the cluster, with one of the following values:</p>
<ul>
<li><code dir="ltr" translate="no">           authentication          </code></li>
<li><code dir="ltr" translate="no">           integrity          </code></li>
<li><code dir="ltr" translate="no">           privacy          </code></li>
</ul>
<p>Example (Bash):<br />
<code dir="ltr" translate="no">          -Dhiveql.rpc.protection=privacy         </code></p>
<p>Example (Windows PowerShell):<br />
<code dir="ltr" translate="no">          "-Dhiveql.rpc.protection=privacy"         </code></p></td>
<td>Required for clusters with enabled Kerberos authentication.</td>
</tr>
</tbody>
</table>

#### Examples

The following example shows how to extract metadata for a Hive 2.3.7 database on a specified host, without authentication and using an alternate port for connection:

``` text
dwh-migration-dumper \
  --connector hiveql \
  --hive-metastore-version 2.3.7 \
  --host host \
  --port port
```

To use Kerberos authentication, sign in as a user that has read permissions to the Hive metastore and generate a Kerberos ticket. Then, generate the metadata zip file with the following command:

``` text
JAVA_OPTS="-Djavax.security.auth.useSubjectCredsOnly=false" \
  dwh-migration-dumper \
  --connector hiveql \
  --host host \
  --port port \
  --hive-kerberos-url principal/kerberos_host
```

### Azure Synapse or Microsoft SQL Server

To allow the `  dwh-migration-dumper  ` tool to connect to Azure Synapse or Microsoft SQL Server, download their JDBC driver from Microsoft's [download page](https://docs.microsoft.com/en-us/sql/connect/jdbc/microsoft-jdbc-driver-for-sql-server?view=sql-server-ver15) .

The following table describes the commonly used flags for extracting Azure Synapse or Microsoft SQL Server metadata by using the extraction tool. For information about all supported flags, see [global flags](#global_flags) .

<table>
<thead>
<tr class="header">
<th><strong>Name</strong></th>
<th><strong>Default value</strong></th>
<th><strong>Description</strong></th>
<th><strong>Required</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">         --connector        </code></td>
<td></td>
<td>The name of the connector to use, in this case <strong>sqlserver</strong> .</td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         --database        </code></td>
<td></td>
<td><p>The name of the database to connect to.</p></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         --driver        </code></td>
<td></td>
<td>The absolute or relative path to the driver JAR file to use for this connection. You can specify multiple driver JAR files, separating them by commas.</td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         --host        </code></td>
<td>localhost</td>
<td>The hostname or IP address of the database server.</td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         --password        </code></td>
<td></td>
<td>The password to use for the database connection.</td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         --port        </code></td>
<td>1433</td>
<td>The port of the database server.</td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         --user        </code></td>
<td></td>
<td>The username to use for the database connection.</td>
<td>Yes</td>
</tr>
</tbody>
</table>

#### Examples

The following example shows how to extract metadata from an Azure Synapse database on a specified host:

``` text
dwh-migration-dumper \
  --connector sqlserver \
  --database database \
  --driver path/mssql-jdbc.jar \
  --host server_name.sql.azuresynapse.net \
  --password password \
  --user user
```

### Greenplum

To allow the `  dwh-migration-dumper  ` tool to connect to Greenplum, download their JDBC driver from VMware Greenplum's [download page](https://docs.vmware.com/en/VMware-Greenplum/7/greenplum-database/datadirect-datadirect_jdbc.html) .

The following table describes the commonly used flags for extracting Greenplum metadata by using the extraction tool. For information about all supported flags, see [global flags](#global_flags) .

<table>
<thead>
<tr class="header">
<th><strong>Name</strong></th>
<th><strong>Default value</strong></th>
<th><strong>Description</strong></th>
<th><strong>Required</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">         --connector        </code></td>
<td></td>
<td>The name of the connector to use, in this case <strong>greenplum</strong> .</td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         --database        </code></td>
<td></td>
<td><p>The name of the database to connect to.</p></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         --driver        </code></td>
<td></td>
<td>The absolute or relative path to the driver JAR file to use for this connection. You can specify multiple driver JAR files, separating them by commas.</td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         --host        </code></td>
<td>localhost</td>
<td>The hostname or IP address of the database server.</td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         --password        </code></td>
<td></td>
<td>The password to use for the database connection.</td>
<td>If not specified, the extraction tool uses a secure prompt to request it.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         --port        </code></td>
<td>5432</td>
<td>The port of the database server.</td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         --user        </code></td>
<td></td>
<td>The username to use for the database connection.</td>
<td>Yes</td>
</tr>
</tbody>
</table>

#### Examples

The following example shows how to extract metadata for a Greenplum database on a specified host:

``` text
dwh-migration-dumper \
  --connector greenplum \
  --database database \
  --driver path/greenplum.jar \
  --host host \
  --password password \
  --user user \
```

### Netezza

To allow the `  dwh-migration-dumper  ` tool to connect to IBM Netezza, you must get their JDBC driver. You can usually get the driver from the `  /nz/kit/sbin  ` directory on your IBM Netezza appliance host. If you can't locate it there, ask your system administrator for help, or read [Installing and Configuring JDBC](https://www.ibm.com/docs/en/psfa/latest?topic=configuration-installing-configuring-jdbc) in the IBM Netezza documentation.

The following table describes the commonly used flags for extracting IBM Netezza metadata by using the extraction tool. For information about all supported flags, see [global flags](#global_flags) .

<table>
<thead>
<tr class="header">
<th><strong>Name</strong></th>
<th><strong>Default value</strong></th>
<th><strong>Description</strong></th>
<th><strong>Required</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">         --connector        </code></td>
<td></td>
<td>The name of the connector to use, in this case <strong>netezza</strong> .</td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         --database        </code></td>
<td></td>
<td><p>A list of the databases to extract, separated by commas.</p></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         --driver        </code></td>
<td></td>
<td>The absolute or relative path to the driver JAR file to use for this connection. You can specify multiple driver JAR files, separating them by commas.</td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         --host        </code></td>
<td>localhost</td>
<td>The hostname or IP address of the database server.</td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         --password        </code></td>
<td></td>
<td>The password to use for the database connection.</td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         --port        </code></td>
<td>5480</td>
<td>The port of the database server.</td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         --user        </code></td>
<td></td>
<td>The username to use for the database connection.</td>
<td>Yes</td>
</tr>
</tbody>
</table>

#### Examples

The following example shows how to extract metadata for two IBM Netezza databases on a specified host:

``` text
dwh-migration-dumper \
  --connector netezza \
  --database database1,database2 \
  --driver path/nzjdbc.jar \
  --host host \
  --password password \
  --user user
```

### PostgreSQL

To allow the `  dwh-migration-dumper  ` tool to connect to PostgreSQL, download their JDBC driver from PostgreSQL's [download page](https://jdbc.postgresql.org/) .

The following table describes the commonly used flags for extracting PostgreSQL metadata by using the extraction tool. For information about all supported flags, see [global flags](#global_flags) .

<table>
<thead>
<tr class="header">
<th><strong>Name</strong></th>
<th><strong>Default value</strong></th>
<th><strong>Description</strong></th>
<th><strong>Required</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">         --connector        </code></td>
<td></td>
<td>The name of the connector to use, in this case <strong>postgresql</strong> .</td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         --database        </code></td>
<td></td>
<td><p>The name of the database to connect to.</p></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         --driver        </code></td>
<td></td>
<td>The absolute or relative path to the driver JAR file to use for this connection. You can specify multiple driver JAR files, separating them by commas.</td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         --host        </code></td>
<td>localhost</td>
<td>The hostname or IP address of the database server.</td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         --password        </code></td>
<td></td>
<td>The password to use for the database connection.</td>
<td>If not specified, the extraction tool uses a secure prompt to request it.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         --port        </code></td>
<td>5432</td>
<td>The port of the database server.</td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         --user        </code></td>
<td></td>
<td>The username to use for the database connection.</td>
<td>Yes</td>
</tr>
</tbody>
</table>

#### Examples

The following example shows how to extract metadata for a PostgreSQL database on a specified host:

``` text
dwh-migration-dumper \
  --connector postgresql \
  --database database \
  --driver path/postgresql-version.jar \
  --host host \
  --password password \
  --user user
```

### Oracle

To allow the `  dwh-migration-dumper  ` tool to connect to Oracle, download their JDBC driver from Oracle's [download page](https://www.oracle.com/database/technologies/appdev/jdbc-downloads.html) .

The following table describes the commonly used flags for extracting Oracle metadata by using the extraction tool. For information about all supported flags, see [global flags](#global_flags) .

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Name</strong></th>
<th><strong>Default value</strong></th>
<th><strong>Description</strong></th>
<th><strong>Required</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">         --connector        </code></td>
<td></td>
<td>The name of the connector to use, in this case <strong>oracle</strong> .</td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         --driver        </code></td>
<td></td>
<td>The absolute or relative path to the driver JAR file to use for this connection. You can specify multiple driver JAR files, separating them by commas.</td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         --host        </code></td>
<td>localhost</td>
<td>The hostname or IP address of the database server.</td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         --oracle-service        </code></td>
<td></td>
<td><p>The Oracle service name to use for the connection.</p></td>
<td>Not explicitly, but you must specify either this flag or the <code dir="ltr" translate="no">         --oracle-sid        </code> flag.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         --oracle-sid        </code></td>
<td></td>
<td><p>The Oracle system identifier (SID) to use for the connection.</p></td>
<td>Not explicitly, but you must specify either this flag or the <code dir="ltr" translate="no">         --oracle-service        </code> flag.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         --password        </code></td>
<td></td>
<td>The password to use for the database connection.</td>
<td>If not specified, the extraction tool uses a secure prompt to request it.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         --port        </code></td>
<td>1521</td>
<td>The port of the database server.</td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         --user        </code></td>
<td></td>
<td><p>The username to use for the database connection.</p>
<p>The user you specify must have the role <code dir="ltr" translate="no">          SELECT_CATALOG_ROLE         </code> in order to extract metadata. To see whether the user has the required role, run the query <code dir="ltr" translate="no">          select granted_role from user_role_privs;         </code> against the Oracle database.</p></td>
<td>Yes</td>
</tr>
</tbody>
</table>

#### Examples

The following example shows how to extract metadata for an Oracle database on a specified host, using the Oracle service for the connection:

``` text
dwh-migration-dumper \
  --connector oracle \
  --driver path/ojdbc8.jar \
  --host host \
  --oracle-service service_name \
  --password password \
  --user user
```

### Snowflake

The following table describes the commonly used flags for extracting Snowflake metadata by using the `  dwh-migration-dumper  ` tool. For information about all supported flags, see [global flags](#global_flags) .

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Name</strong></th>
<th><strong>Default value</strong></th>
<th><strong>Description</strong></th>
<th><strong>Required</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">         --assessment        </code></td>
<td></td>
<td><p>Turns on assessment mode when generating database logs or extracting metadata. The <code dir="ltr" translate="no">          dwh-migration-dumper         </code> tool generates required metadata statistics for BigQuery migration assessment when used for metadata extraction. When used for query logs, the tool extracts additional columns for BigQuery migration assessment.</p></td>
<td>Only for assessment.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         --connector        </code></td>
<td></td>
<td>The name of the connector to use, in this case <strong>snowflake</strong> .</td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         --database        </code></td>
<td></td>
<td><p>The name of the database to extract.</p>
<p>You can only extract from one database at a time from Snowflake. This flag is not allowed in assessment mode.</p></td>
<td>Only for translation.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         --host        </code></td>
<td>localhost</td>
<td>The hostname or IP address of the database server.</td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         --private-key-file        </code></td>
<td></td>
<td><p>The path to the RSA private key used for authentication. We recommend using a <a href="https://docs.snowflake.com/en/user-guide/admin-user-management#types-of-users"><code dir="ltr" translate="no">           SERVICE          </code></a> user with a key-pair based authentication. This provides the secure method for accessing Snowflake data platform without a need to generate MFA tokens.</p></td>
<td>No, if not provided extraction tool uses a password based authentication.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         --private-key-password        </code></td>
<td></td>
<td><p>The password that was used when creating the RSA private key.</p></td>
<td>No, it is required only if the private key is encrypted.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         --password        </code></td>
<td></td>
<td>The password to use for the database connection.</td>
<td>If not specified, the extraction tool uses a secure prompt to request it. However, we recommend using key-pair based authentication instead.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         --query-log-start        </code></td>
<td></td>
<td><p>The start time (inclusive) for query logs to extract. The value is truncated to the hour. This flag is only available for the <code dir="ltr" translate="no">          snowflake-logs         </code> connector.</p>
<p>Example: <code dir="ltr" translate="no">          --query-log-start "2023-01-01 14:00:00"         </code></p></td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         --query-log-end        </code></td>
<td></td>
<td><p>The end time (exclusive) for query logs to extract. The value is truncated to the hour. This flag is only available for the <code dir="ltr" translate="no">          snowflake-logs         </code> connector.</p>
<p>Example: <code dir="ltr" translate="no">          --query-log-end "2023-01-15 22:00:00"         </code></p></td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         --role        </code></td>
<td></td>
<td>The Snowflake role to use for authorization. You only need to specify this for large installations where you need to get metadata from the <code dir="ltr" translate="no">         SNOWFLAKE.ACCOUNT_USAGE        </code> schema instead of <code dir="ltr" translate="no">         INFORMATION_SCHEMA        </code> . For more information, see <a href="#large-instance">Working with large Snowflake instances</a> .</td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         --user        </code></td>
<td></td>
<td><p>The username to use for the database connection.</p></td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         --warehouse        </code></td>
<td></td>
<td><p>The Snowflake warehouse to use for processing metadata queries.</p></td>
<td>Yes</td>
</tr>
</tbody>
</table>

#### Examples

The following example shows how to extract metadata for assessment:

``` text
dwh-migration-dumper \
  --connector snowflake \
  --assessment \
  --host "account.snowflakecomputing.com" \
  --role role \
  --user user \
  --private-key-file private-key-file \
  --private-key-password private-key-password \
  --warehouse warehouse
```

The following example shows how to extract metadata for a typically sized Snowflake database on the local host:

``` text
dwh-migration-dumper \
  --connector snowflake \
  --database database \
  --user user \
  --private-key-file private-key-file \
  --private-key-password private-key-password \
  --warehouse warehouse
```

The following example shows how to extract metadata for a large Snowflake database on a specified host:

``` text
dwh-migration-dumper \
  --connector snowflake \
  --database database \
  --host "account.snowflakecomputing.com" \
  --role role \
  --user user \
  --private-key-file private-key-file \
  --private-key-password private-key-password \
  --warehouse warehouse
```

Alternatively, you can use the following example to extract metadata using password-based authentication:

``` text
dwh-migration-dumper \
  --connector snowflake \
  --database database \
  --host "account.snowflakecomputing.com" \
  --password password \
  --user user \
  --warehouse warehouse
```

#### Working with large Snowflake instances

The `  dwh-migration-dumper  ` tool reads metadata from the Snowflake `  INFORMATION_SCHEMA  ` . However, there is a limit to the amount of data you can retrieve from `  INFORMATION_SCHEMA  ` . If you run the extraction tool and receive the error `  SnowflakeSQLException: Information schema query returned too much data  ` , you must take the following steps so that you can read metadata from the `  SNOWFLAKE.ACCOUNT_USAGE  ` schema instead:

1.  Open the **Shares** option in the Snowflake web interface.

2.  Create a database from the `  SNOWFLAKE.ACCOUNT_USAGE  ` share:
    
    ``` text
    -- CREATE DATABASE database FROM SHARE SNOWFLAKE.ACCOUNT_USAGE;
    ```

3.  Create a role:
    
    ``` text
    CREATE ROLE role;
    ```

4.  Grant `  IMPORTED  ` privileges on the new database to the role:
    
    ``` text
    GRANT IMPORTED PRIVILEGES ON DATABASE database TO ROLE role;
    ```

5.  Grant the role to the user you intend to use to run the `  dwh-migration-dumper  ` tool:
    
    ``` text
    GRANT ROLE role TO USER user;
    ```

### Vertica

To allow the `  dwh-migration-dumper  ` tool to connect to Vertica, download their JDBC driver from their [download page](https://www.vertica.com/download/vertica/client-drivers/) .

The following table describes the commonly used flags for extracting Vertica metadata by using the extraction tool. For information about all supported flags, see [global flags](#global_flags) .

<table>
<thead>
<tr class="header">
<th><strong>Name</strong></th>
<th><strong>Default value</strong></th>
<th><strong>Description</strong></th>
<th><strong>Required</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">         --connector        </code></td>
<td></td>
<td>The name of the connector to use, in this case <strong>vertica</strong> .</td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         --database        </code></td>
<td></td>
<td><p>The name of the database to connect to.</p></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         --driver        </code></td>
<td></td>
<td>The absolute or relative path to the driver JAR file to use for this connection. You can specify multiple driver JAR files, separating them by commas.</td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         --host        </code></td>
<td>localhost</td>
<td>The hostname or IP address of the database server.</td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         --password        </code></td>
<td></td>
<td>The password to use for the database connection.</td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         --port        </code></td>
<td>5433</td>
<td>The port of the database server.</td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         --user        </code></td>
<td></td>
<td>The username to use for the database connection.</td>
<td>Yes</td>
</tr>
</tbody>
</table>

#### Examples

The following example shows how to extract metadata from a Vertica database on the local host:

``` text
dwh-migration-dumper \
  --driver path/vertica-jdbc.jar \
  --connector vertica \
  --database database
  --user user
  --password password
```

### BigQuery

The following table describes the commonly used flags for extracting BigQuery metadata by using the extraction tool. For information about all supported flags, see [global flags](#global_flags) .

<table>
<thead>
<tr class="header">
<th><strong>Name</strong></th>
<th><strong>Default value</strong></th>
<th><strong>Description</strong></th>
<th><strong>Required</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">         --connector        </code></td>
<td></td>
<td>The name of the connector to use, in this case <strong>bigquery</strong> .</td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         --database        </code></td>
<td></td>
<td><p>The list of projects to extract metadata and query logs from, separated by commas.</p></td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         --schema        </code></td>
<td></td>
<td><p>The list of datasets to extract metadata and query logs from, separated by commas.</p></td>
<td>Yes</td>
</tr>
</tbody>
</table>

#### Examples

The following example shows how to extract metadata from a Vertica database on the local host:

``` text
dwh-migration-dumper \
  --connector bigquery \
  --database PROJECT1, PROJECT2
  --schema DATASET1, DATASET2
```

## Global flags

The following table describes the flags that can be used with any of the supported source platforms.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Name</strong></th>
<th><strong>Description</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       --connector      </code></td>
<td>The connector name for the source system.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       --database      </code></td>
<td>Usage varies by source system.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       --driver      </code></td>
<td>The absolute or relative path to the driver JAR file to use when connecting to the source system. You can specify multiple driver JAR files, separating them by commas.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       --dry-run      </code> or <code dir="ltr" translate="no">       -n      </code></td>
<td>Show what actions the extraction tool would make without executing them.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       --help      </code></td>
<td>Displays command-line help.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       --host      </code></td>
<td>The hostname or IP address of the database server to connect to.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       --jdbcDriverClass      </code></td>
<td>Optionally overrides the vendor-specified JDBC driver class name. Use this if you have a custom JDBC client.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       --output      </code></td>
<td>The path of the output zip file. For example, <code dir="ltr" translate="no">       dir1/dir2/teradata-metadata.zip      </code> . If you don't specify a path, the output file is created in your working directory. If you specify the path to a directory, the default zip filename is created in the specified directory. If the directory does not exist, it is created.
<p>To use Cloud Storage, use the following format:<br />
<code dir="ltr" translate="no">        gs://&lt;BUCKET&gt;/&lt;PATH&gt;       </code> .</p>
<p>To authenticate using Google Cloud credentials, see <a href="/docs/authentication/client-libraries">Authenticate for using client libraries</a> .</p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       --password      </code></td>
<td>The password to use for the database connection.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       --port      </code></td>
<td>The port of the database server.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       --save-response-file      </code></td>
<td>Saves your command line flags in a JSON file for easy re-use. The file is named <code dir="ltr" translate="no">       dumper-response-file.json      </code> and is created in the working directory. To use the response file, provide the path to it prefixed by <code dir="ltr" translate="no">       @      </code> when you run the extraction tool, for example <code dir="ltr" translate="no">       dwh-migration-dumper @path/to/dumper-response-file.json      </code> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       --schema      </code></td>
<td><p>A list of the schemas to extract, separated by commas.</p>
<p>Oracle doesn't differentiate between a <a href="https://docs.oracle.com/cd/B19306_01/server.102/b14196/schema.htm#CFHHBEGH">schema</a> and the database user who created the schema, so you can use either schema names or user names with the <code dir="ltr" translate="no">        --schema       </code> flag. For example, <code dir="ltr" translate="no">        --schema schema1,user2,schema3       </code> .</p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       --thread-pool-size      </code></td>
<td><p>Sets the thread pool size, which affects the connection pool size. The default size of the thread pool is the number of cores on the server running the <code dir="ltr" translate="no">        dwh-migration-dumper       </code> tool.</p>
<p>If the extraction tool seems slow or otherwise in need of more resources, you can raise the number of threads used. If there are indications that other processes on the server require more bandwidth, you can lower the number of threads used.</p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       --url      </code></td>
<td><p>The URL to use for the database connection, instead of the URI generated by the JDBC driver.</p>
<p>The generated URI should be sufficient in most cases. Only override the generated URI when you need to use a JDBC connection setting that is specific to the source platform and is not already set by one of the flags listed in this table.</p></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       --user      </code></td>
<td>The username to use for the database connection.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       --version      </code></td>
<td>Displays the product version.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       --telemetry      </code></td>
<td><p>Collects insights into the performance characteristics of runs, such as duration, run counts, and resource usage. This is enabled by default. To disable telemetry, set this flag to <code dir="ltr" translate="no">        false       </code> .</p></td>
</tr>
</tbody>
</table>

## Troubleshooting

This section explains some common issues and troubleshooting techniques for the `  dwh-migration-dumper  ` tool.

### Out of memory error

The `  java.lang.OutOfMemoryError  ` error in the `  dwh-migration-dumper  ` tool terminal output is often related to insufficient memory for processing retrieved data. To address this issue, increase available memory or reduce the number of processing threads.

You can increase maximum memory by exporting the `  JAVA_OPTS  ` environment variable:

### Linux

``` text
export JAVA_OPTS="-Xmx4G"
```

### Windows

``` text
set JAVA_OPTS="-Xmx4G"
```

You can reduce the number of processing threads (default is 32) by including the `  --thread-pool-size  ` flag. This option is supported for `  hiveql  ` and `  redshift*  ` connectors only.

``` text
dwh-migration-dumper --thread-pool-size=1
```

### Handling a `     WARN...Task failed    ` error

You might sometimes see a `  WARN [main] o.c.a.d.MetadataDumper [MetadataDumper.java:107] Task failed: …  ` error in the `  dwh-migration-dumper  ` tool terminal output. The extraction tool submits multiple queries to the source system, and the output of each query is written to its own file. Seeing this issue indicates that one of these queries failed. However, failure of one query doesn't prevent the execution of the other queries. If you see more than a couple of `  WARN  ` errors, review the issue details and see if there is anything that you need to correct in order for the query to run appropriately. For example, if the database user you specified when running the extraction tool lacks permissions to read all metadata, try again with a user with the correct permissions.

### Corrupted ZIP file

To validate the `  dwh-migration-dumper  ` tool zip file, download the [`  SHA256SUMS.txt  ` file](https://github.com/google/dwh-migration-tools/releases/latest/download/SHA256SUMS.txt) and run the following command:

### Bash

``` text
sha256sum --check SHA256SUMS.txt
```

The `  OK  ` result confirms successful checksum verification. Any other message indicates verification error:

  - `  FAILED: computed checksum did NOT match  ` : the zip file is corrupted and has to be downloaded again.
  - `  FAILED: listed file could not be read  ` : the zip file version can't be located. Make sure the checksum and zip files are downloaded from the same release version and placed in the same directory.

### Windows PowerShell

``` text
(Get-FileHash RELEASE_ZIP_FILENAME).Hash -eq ((Get-Content SHA256SUMS.txt) -Split " ")[0]
```

Replace the `  RELEASE_ZIP_FILENAME  ` with the downloaded zip filename of the `  dwh-migration-dumper  ` command-line extraction tool release—for example, `  dwh-migration-tools-v1.0.52.zip  `

The `  True  ` result confirms successful checksum verification.

The `  False  ` result indicates verification error. Make sure the checksum and zip files are downloaded from the same release version and placed in the same directory.

### Teradata query logs extraction is slow

To improve performance of joining tables that are specified by the `  -Dteradata-logs.query-logs-table  ` and `  -Dteradata-logs.sql-logs-table  ` flags, you can include an additional column of type `  DATE  ` in the `  JOIN  ` condition. This column must be defined in both tables and it must be part of the Partitioned Primary Index. To include this column, use the `  -Dteradata-logs.log-date-column  ` flag.

Example:

### Bash

``` text
dwh-migration-dumper \
  -Dteradata-logs.query-logs-table=historicdb.ArchivedQryLogV \
  -Dteradata-logs.sql-logs-table=historicdb.ArchivedDBQLSqlTbl \
  -Dteradata-logs.log-date-column=ArchiveLogDate
```

### Windows PowerShell

``` text
dwh-migration-dumper `
  "-Dteradata-logs.query-logs-table=historicdb.ArchivedQryLogV" `
  "-Dteradata-logs.sql-logs-table=historicdb.ArchivedDBQLSqlTbl" `
  "-Dteradata-logs.log-date-column=ArchiveLogDate"
```

### Teradata row size limit exceeded

Teradata 15 has a 64kB row size limit. If the limit is exceeded, the dumper fails with the following message: `  none [Error 9804] [SQLState HY000] Response Row size or Constant Row size overflow  `

To resolve this error, either extend the row limit to 1MB or split the rows into multiple rows:

  - Install and enable the 1MB Perm and Response Rows feature and current TTU software. For more information, see [Teradata Database Message 9804](https://docs.teradata.com/r/Teradata-VantageCloud-Lake-Analytics-Database-Messages/Database-Messages/9804)
  - Split the long query text into multiple rows by using the `  -Dteradata.metadata.max-text-length  ` and `  -Dteradata-logs.max-sql-length  ` flags.

The following command shows the usage of the `  -Dteradata.metadata.max-text-length  ` flag to split the long query text into multiple rows of at most 10000 characters each:

### Bash

``` text
dwh-migration-dumper \
  --connector teradata \
  -Dteradata.metadata.max-text-length=10000
```

### Windows PowerShell

``` text
dwh-migration-dumper `
  --connector teradata `
  "-Dteradata.metadata.max-text-length=10000"
```

The following command shows the usage of the `  -Dteradata-logs.max-sql-length  ` flag to split the long query text into multiple rows of at most 10000 characters each:

### Bash

``` text
dwh-migration-dumper \
  --connector teradata-logs \
  -Dteradata-logs.max-sql-length=10000
```

### Windows PowerShell

``` text
dwh-migration-dumper `
  --connector teradata-logs `
  "-Dteradata-logs.max-sql-length=10000"
```

### Oracle connection issue

In common cases like invalid password or hostname, `  dwh-migration-dumper  ` tool prints a meaningful error message describing the root issue. However, in some cases, the error message returned by the Oracle server may be generic and difficult to investigate.

One of these issues is `  IO Error: Got minus one from a read call  ` . This error indicates that the connection to Oracle server has been established but the server did not accept the client and closed the connection. This issue typically occurs when the server accepts `  TCPS  ` connections only. By default, `  dwh-migration-dumper  ` tool uses the `  TCP  ` protocol. To solve this issue you must override the Oracle JDBC connection URL.

Instead of providing the `  oracle-service  ` , `  host  ` and `  port  ` flags, you can resolve this issue by providing the `  url  ` flag in the following format: `  jdbc:oracle:thin:@tcps://{HOST_NAME}:{PORT}/{ORACLE_SERVICE}  ` . Typically, the `  TCPS  ` port number used by the Oracle server is `  2484  ` .

Example dumper command:

``` text
  dwh-migration-dumper \
    --connector oracle-stats \
    --url "jdbc:oracle:thin:@tcps://host:port/oracle_service" \
    --assessment \
    --driver "jdbc_driver_path" \
    --user "user" \
    --password
```

In addition to changing connection protocol to TCPS you might need to provide the trustStore SSL configuration that is required to verify Oracle server certificate. A missing SSL configuration will result in an `  Unable to find valid certification path  ` error message. To resolve this, set the JAVA\_OPTS environment variable:

``` text
  set JAVA_OPTS=-Djavax.net.ssl.trustStore="jks_file_location" -Djavax.net.ssl.trustStoreType=JKS -Djavax.net.ssl.trustStorePassword="password"
```

Depending on your Oracle server configuration, you might also need to provide the keyStore configuration. See [SSL With Oracle JDBC Driver](https://www.oracle.com/docs/tech/wp-oracle-jdbc-thin-ssl.pdf) for more information about configuration options.

## What's next

After you run the `  dwh-migration-dumper  ` tool, [upload the output](/bigquery/docs/batch-sql-translator#upload-files) to Cloud Storage along with the source files for translation.
