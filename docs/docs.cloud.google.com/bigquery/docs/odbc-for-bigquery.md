---
name: documents/docs.cloud.google.com/bigquery/docs/odbc-for-bigquery
uri: https://docs.cloud.google.com/bigquery/docs/odbc-for-bigquery
title: Use the ODBC driver for BigQuery
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
update_time: "2026-05-09T04:50:04Z"
---

# Use the ODBC driver for BigQuery

> **Preview**
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

> **Note:** ODBC driver for BigQuery is available under the Apache 2.0 [license](https://www.apache.org/licenses/LICENSE-2.0) . To request feedback or support for this feature, send an email to <bigquery-drivers-feedback@google.com> .

The Open Database Connectivity (ODBC) driver for BigQuery connects your applications to BigQuery. This lets you use BigQuery features with your preferred tooling and infrastructure.

## Before you begin

1.  Make sure that you're familiar with [Open Database Connectivity (ODBC) drivers](https://learn.microsoft.com/en-us/sql/odbc/reference/what-is-odbc) and the driver manager.

2.  Take note of the following system requirements:
    
    <table>
    <colgroup>
    <col style="width: 33%" />
    <col style="width: 33%" />
    <col style="width: 33%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th><strong>Operating System</strong></th>
    <th><strong>Supported Architectures</strong></th>
    <th><strong>Minimum Version and Dependencies</strong></th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Windows</td>
    <td>32-bit (x86), 64-bit (x64)</td>
    <td>Version: Windows 10, Windows Server 2016 or newer<br />
    Dependency: Microsoft Visual C++ Redistributable for Visual Studio 2019 or 2022</td>
    </tr>
    <tr class="even">
    <td>macOS</td>
    <td>64-bit (x86_64), ARM64 (Apple Silicon)</td>
    <td>Version: macOS 12 (Monterey) or newer<br />
    Dependency: An ODBC Driver Manager (for example, <a href="https://www.unixodbc.org/">unixODBC</a> ). Ensure you add the installation directory to your <code dir="ltr" translate="no">DYLD_LIBRARY_PATH</code> .</td>
    </tr>
    <tr class="odd">
    <td>Linux</td>
    <td>64-bit (x86_64)</td>
    <td>Version: Any distribution with glibc 2.27 or later (for example, Ubuntu 20.04 LTS+, Debian 11+)<br />
    Dependency: An ODBC Driver Manager (for example, <a href="https://www.unixodbc.org/">unixODBC</a> ). Ensure you add the installation directory to your <code dir="ltr" translate="no">LD_LIBRARY_PATH</code> .</td>
    </tr>
    </tbody>
    </table>

3.  Identify your connection type for the ODBC driver for BigQuery. The driver supports the following authentication methods:
    
    **Authentication method**

## Install and configure the ODBC driver

This section describes how to install and configure the ODBC driver for Windows and non-Windows operating systems.

### Windows

On Windows, ensure you install the driver architecture that matches your application's architecture. For example, use the 64-bit driver for 64-bit applications and the 32-bit driver for 32-bit applications. A 64-bit Windows system supports both 32-bit and 64-bit applications.

  - Download [`ODBCDriverforBigQuery_windows_x86.msi`](https://storage.googleapis.com/bq-driver-releases/odbc/ODBCDriverforBigQuery_windows_x86_latest.msi) for 32-bit applications
  - Download [`ODBCDriverforBigQuery_windows_x64.msi`](https://storage.googleapis.com/bq-driver-releases/odbc/ODBCDriverforBigQuery_windows_x64_latest.msi) for 64-bit applications

#### Create a Data Source Name

To create a Data Source Name in Windows:

1.  From the **Start** menu, go to **ODBC Data Sources** , and select the version that has the same bitness as your client application to ensure proper connection to BigQuery.
2.  In the ODBC Data Source Administrator, click the **Drivers** tab.
3.  Locate the **ODBC Driver for BigQuery** as it appears in the alphabetical list of installed ODBC drivers.
4.  Choose one of the following options:
      - To create a DSN for the current user, click the **User DSN** tab.
      - To create a DSN for all users, click the **System DSN** tab. System DSNs are recommended because some applications load data using different user accounts and might not detect User DSNs created under another user account.
5.  Click **Add** .
6.  In the **Create New Data Source** dialog, select **ODBC Driver for BigQuery** and then click **Finish** .
7.  The **ODBC Driver for BigQuery DSN Setup** dialog opens.
8.  In the **Data Source Name** field, type a name for your DSN.
9.  See the [Connection Properties](https://docs.cloud.google.com/bigquery/docs/odbc-for-bigquery#connection_properties) section to understand what values to populate.

### Non-Windows

64-bit Linux distributions support both 32-bit and 64-bit applications. Ensure the ODBC driver's architecture matches the application you intend to use. For example, use the 64-bit driver for 64-bit applications and the 32-bit driver for 32-bit applications. You can install both driver architectures simultaneously on a single system.

  - Download [`ODBCDriverforBigQuery_linux_latest.zip`](https://storage.googleapis.com/bq-driver-releases/odbc/ODBCDriverforBigQuery_linux_latest.zip) for Linux
  - Download [`ODBCDriverforBigQuery_macos_latest.tar.gz`](https://storage.googleapis.com/bq-driver-releases/odbc/ODBCDriverforBigQuery_macos_latest.tar.gz) for macOS

To install the connector using the tar or zip file package:

1.  Create the directory where you want to install the connector, if it does not already exist.
2.  Extract the main zip file to a convenient temporary location.
3.  Navigate to the folder of the extracted tar or zip file and then (optionally) copy all the files and folders to the installation directory.
4.  After extraction, the ODBC Driver for BigQuery shared object path is `[INSTALLDIR]/lib/libgoogle_cloud_odbc_bq_driver.so` . Update your `.ini` files to reflect the correct path of the connector.

<!-- end list -->

    unzip linux_odbc-driver.VERSION.zip -d linux_odbc-driver.VERSION/
    cd ./linux_odbc-driver.VERSION
    export INSTALL_DIR=$(pwd)
    export ODBCINI=$INSTALL_DIR/odbc.ini
    export ODBCINSTINI=$INSTALL_DIR/odbcinst.ini
    export GOOGLEBIGQUERYODBCINI=$INSTALL_DIR/googlebigqueryodbc.ini

## Establish a connection

To establish a connection using the ODBC driver for BigQuery, you can use a connection string or a DSN.

### Connection string format

    Driver=ODBC Driver for BigQuery;ProjectId=PROJECT_ID;OAuthMechanism=AUTH_TYPE;AUTH_PROPS;OTHER_PROPS

Replace the following:

  - `PROJECT_ID` : the ID of your BigQuery project.
  - `AUTH_TYPE` : a number specifying the type of authentication you used. Choose one of the following:
      - `0` : for service account authentication
      - `3` : for Application Default Credential authentication
      - `4` : for Workload or Workforce Identity Federation authentication
  - `AUTH_PROPS` : the authentication information you noted when you authenticated to BigQuery.
  - `OTHER_PROPS` (optional): additional connection properties for the ODBC driver.

### Connection properties

ODBC driver connection properties are configuration parameters that you include in the connection string when you [establish a connection](https://docs.cloud.google.com/bigquery/docs/odbc-for-bigquery#establish_a_connection) to a database. The ODBC driver for BigQuery supports the following connection properties.

> **Note:** All connection property names are case-insensitive.

<table>
<colgroup>
<col style="width: 15%" />
<col style="width: 40%" />
<col style="width: 15%" />
<col style="width: 15%" />
<col style="width: 15%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Connection property</strong></th>
<th><strong>Description</strong></th>
<th><strong>Default value</strong></th>
<th><strong>Data type</strong></th>
<th><strong>Required</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">AdditionalProjects</code></td>
<td>Projects that the driver can access for queries and metadata operations, in addition to the primary project set by the <code dir="ltr" translate="no">ProjectId</code> property.</td>
<td>N/A</td>
<td>Comma-separated string</td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">AllowHtapiForLargeResults</code></td>
<td>Determines whether the driver can use the Read API.</td>
<td><code dir="ltr" translate="no">0</code></td>
<td>Boolean</td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">AllowLargeResults</code></td>
<td>Specifies whether the ODBC Driver should process query results greater than 128MB when using legacy SQL ( <code dir="ltr" translate="no">QueryDialect=BIG_QUERY</code> ).</td>
<td><code dir="ltr" translate="no">0</code></td>
<td>Boolean</td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">BYOID_AudienceUrl</code></td>
<td>Audience contains the resource name for the Workload Identity Pool or the Workforce Pool and the provider identifier in that pool.</td>
<td>N/A</td>
<td>String</td>
<td>Only when <code dir="ltr" translate="no">OAuthMechanism=4</code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">BYOID_CredentialSource</code></td>
<td>Sets the necessary information to retrieve the token itself, as well as some environmental information.</td>
<td>N/A</td>
<td>String</td>
<td>Only when <code dir="ltr" translate="no">OAuthMechanism=4</code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">BYOID_PoolUserProject</code></td>
<td>Set this when it is a Workforce Pool and not a Workload Identity Pool.</td>
<td>N/A</td>
<td>String</td>
<td>Only when <code dir="ltr" translate="no">OAuthMechanism=4</code> and using a Workforce Pool</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">BYOID_SubjectTokenType</code></td>
<td>Sets the STS token type based on the Oauth2.0 token exchange specification. Expected values include:<br />

<ul>
<li><code dir="ltr" translate="no">urn:ietf:params:oauth:token-type:jwt</code></li>
<li><code dir="ltr" translate="no">urn:ietf:params:oauth:token-type:id_token</code></li>
<li><code dir="ltr" translate="no">urn:ietf:params:oauth:token-type:saml2</code></li>
<li><code dir="ltr" translate="no">urn:ietf:params:aws:token-type:aws4_request</code></li>
</ul></td>
<td>N/A</td>
<td>String</td>
<td>Only when <code dir="ltr" translate="no">OAuthMechanism=4</code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">BYOID_TokenUrl</code></td>
<td>Sets the STS token exchange endpoint.</td>
<td><code dir="ltr" translate="no">https://sts.googleapis.com/v1/token</code></td>
<td>String</td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">DefaultDataset</code></td>
<td>Serves as a designated dataset within a project that the driver automatically references when you execute queries without explicitly specifying a dataset.</td>
<td>N/A</td>
<td>String</td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">FilterTablesOnDefaultDataset</code></td>
<td>Determines the scope of metadata that table/column metadata methods return. When FALSE, no filtering occurs. You must also set the <code dir="ltr" translate="no">DefaultDataset</code> property to enable filtering.</td>
<td><code dir="ltr" translate="no">FALSE</code></td>
<td>Boolean</td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">EnableSession</code></td>
<td>Determines whether a connection starts a session. When enabled, the first query run by that particular connection starts a session and the driver passes the session ID to all subsequent queries.</td>
<td><code dir="ltr" translate="no">0</code></td>
<td>Boolean</td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">JobCreationMode</code></td>
<td>Lets you enable the low latency query path. Choose one of the following:<br />

<ul>
<li><code dir="ltr" translate="no">1</code> : The driver creates jobs for every query (JOB_CREATION_REQUIRED)</li>
<li><code dir="ltr" translate="no">2</code> : The driver executes queries without jobs (JOB_CREATION_OPTIONAL)</li>
</ul></td>
<td><code dir="ltr" translate="no">2</code></td>
<td>Integer</td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">KeyFilePath</code></td>
<td>The path to the service account key when using service account authentication.</td>
<td>N/A</td>
<td>String</td>
<td>Only when <code dir="ltr" translate="no">OAuthMechanism=0</code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">KMSKeyName</code></td>
<td>Lets you specify the name of the KMS key to use when encrypting and decrypting data.</td>
<td>N/A</td>
<td>String</td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">LargeResultsDataSetId</code></td>
<td>Lets you specify the destination dataset for storing large query results.</td>
<td>N/A</td>
<td>String</td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">LargeResultsDatasetExpirationTime</code></td>
<td>Lets you specify the lifetime of all tables in the large results dataset, in milliseconds.</td>
<td><code dir="ltr" translate="no">3600000</code></td>
<td>Long</td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">Location</code></td>
<td>Lets you specify the location where the driver creates or queries datasets.</td>
<td>N/A</td>
<td>String</td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">LogLevel</code></td>
<td>Limits the detail the driver logs during interactions. Choose one of the following:<br />

<ul>
<li><code dir="ltr" translate="no">0</code> : <code dir="ltr" translate="no">OFF</code></li>
<li><code dir="ltr" translate="no">1</code> : <code dir="ltr" translate="no">ERROR</code></li>
<li><code dir="ltr" translate="no">2</code> : <code dir="ltr" translate="no">WARNING</code></li>
<li><code dir="ltr" translate="no">3</code> : <code dir="ltr" translate="no">INFO</code></li>
</ul></td>
<td><code dir="ltr" translate="no">0</code></td>
<td>Integer</td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">LogPath</code></td>
<td>Lets you specify the directory where the driver writes log files.</td>
<td>N/A</td>
<td>String</td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">LogFileCount</code></td>
<td>Lets you set the maximum number of log files to keep.</td>
<td><code dir="ltr" translate="no">0</code></td>
<td>Integer</td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">LogFileSize</code></td>
<td>Lets you set the maximum size of each log file in bytes.</td>
<td><code dir="ltr" translate="no">0</code></td>
<td>Long</td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">MaxResults</code></td>
<td>Lets you specify the number of results per page in BigQuery API Result.</td>
<td><code dir="ltr" translate="no">10000</code></td>
<td>Long</td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">MaxThreads</code></td>
<td>Defines the maximum number of threads that the connector can use for concurrent processing in a thread pool. To configure this property as a connector-wide setting for non-Windows (Linux/macOS) connectors, you specify it in the <code dir="ltr" translate="no">googlebigqueryodbc.ini</code> file.</td>
<td><code dir="ltr" translate="no">8</code></td>
<td>Integer</td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">OAuthMechanism</code></td>
<td>The authentication type. Choose one of the following:<br />

<ul>
<li><code dir="ltr" translate="no">0</code> : service account authentication</li>
<li><code dir="ltr" translate="no">3</code> : Application Default Credential authentication</li>
<li><code dir="ltr" translate="no">4</code> : Workload or Workforce Identity Federation authentication</li>
</ul></td>
<td>N/A</td>
<td>Integer</td>
<td>Yes</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">ProjectId</code></td>
<td>The default project ID for the driver. The driver uses this project to execute queries and bills it for resource usage.</td>
<td>N/A</td>
<td>String</td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">ProxyHost</code></td>
<td>Hostname or IP address of a proxy server.</td>
<td>N/A</td>
<td>String</td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">ProxyPort</code></td>
<td>Port number on which the proxy server is listening.</td>
<td>N/A</td>
<td>String</td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">ProxyPwd</code></td>
<td>Password for authentication when connecting through a proxy server.</td>
<td>N/A</td>
<td>String</td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">ProxyUid</code></td>
<td>Username for authentication when connecting through a proxy server.</td>
<td>N/A</td>
<td>String</td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">PrivateServiceConnectUris</code></td>
<td>Custom endpoints to overwrite default endpoints. Examples:
<ul>
<li><code dir="ltr" translate="no">BIGQUERY=https://bigquery.us-east4.rep.googleapis.com/</code></li>
<li><code dir="ltr" translate="no">READ_API=bigquerystorage.us-east4.rep.googleapis.com</code></li>
<li><code dir="ltr" translate="no">OAUTH2=oauth2.us-east4.rep.googleapis.com</code></li>
</ul></td>
<td>N/A</td>
<td>Comma-separated string</td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">QueryDialect</code></td>
<td>Specifies which query dialect to use. Use <code dir="ltr" translate="no">SQL</code> for GoogleSQL (highly recommended) and <code dir="ltr" translate="no">BIG_QUERY</code> for legacy SQL.</td>
<td><code dir="ltr" translate="no">SQL</code></td>
<td>String</td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">QueryProperties</code></td>
<td>Configures properties which can modify the query behavior.</td>
<td>N/A</td>
<td>Map&lt;String, String&gt;</td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">UniverseDomain</code></td>
<td>Specifies the universe domain for your organization.</td>
<td><code dir="ltr" translate="no">googleapis.com</code></td>
<td>String</td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">UseQueryCache</code></td>
<td>Lets you enable the query caching feature in BigQuery.</td>
<td><code dir="ltr" translate="no">true</code></td>
<td>Boolean</td>
<td>No</td>
</tr>
</tbody>
</table>

## Run queries with the driver

This section provides information on data type mapping and examples for running queries with the ODBC driver.

### Data type mapping

When you run queries through the ODBC driver for BigQuery, the following data type mapping occurs (based on standard ODBC SQL types):

| **GoogleSQL type** | **ODBC SQL type**    |
| ------------------ | -------------------- |
| `INT64`            | `SQL_BIGINT`         |
| `BOOL`             | `SQL_BIT`            |
| `DATE`             | `SQL_TYPE_DATE`      |
| `FLOAT64`          | `SQL_DOUBLE`         |
| `TIME`             | `SQL_TYPE_TIME`      |
| `TIMESTAMP`        | `SQL_TYPE_TIMESTAMP` |
| `DATETIME`         | `SQL_TYPE_TIMESTAMP` |
| `BYTES`            | `SQL_VARBINARY`      |
| `STRING`           | `SQL_VARCHAR`        |
| `ARRAY`            | `SQL_VARCHAR`        |
| `STRUCT`           | `SQL_VARCHAR`        |
| `INTERVAL`         | `SQL_VARCHAR`        |
| `JSON`             | `SQL_VARCHAR`        |
| `GEOGRAPHY`        | `SQL_VARCHAR`        |
| `RANGE`            | `SQL_VARCHAR`        |
| `NUMERIC`          | `SQL_NUMERIC`        |
| `BIGNUMERIC`       | `SQL_NUMERIC`        |

### Examples

The following examples demonstrate how to use parameterized queries and multi-statement scripts with the ODBC driver.

#### Parameterized queries

    // 1. Prepare statement
    std::string insert_stmt = "INSERT INTO MyTable VALUES (?, ?, ?)";
    status = SQLPrepare(hstmt, (SQLCHAR*)insert_stmt.c_str(), SQL_NTS);
    
    // 2. Bind parameters
    std::string str_val = "example_string";
    long long int_val = 12345;
    double float_val = 1.2345;
    
    // Bind string field
    status = SQLBindParameter(
        hstmt, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_VARCHAR, 50, 0,
        (SQLPOINTER)str_val.c_str(), str_val.size(), NULL);
    
    // Bind integer field
    status = SQLBindParameter(
        hstmt, 2, SQL_PARAM_INPUT, SQL_C_UBIGINT, SQL_BIGINT, 0, 0,
        &int_val, 0, NULL);
    
    // Bind float field
    status = SQLBindParameter(
        hstmt, 3, SQL_PARAM_INPUT, SQL_C_DOUBLE, SQL_DOUBLE, 0, 0,
        &float_val, 0, NULL);
    
    // 3. Execute statement
    status = SQLExecute(hstmt);

#### Multi-statement scripts

    // 1. Prepare and execute the multi-statement script
    std::string query =
        "CREATE OR REPLACE TABLE MyTable (StringField STRING, IntegerField INTEGER); "
        "INSERT INTO MyTable VALUES ('example', 123); "
        "SELECT * FROM MyTable;";
    
    status = SQLExecDirect(hstmt, (SQLCHAR*)query.c_str(), SQL_NTS);
    
    // 2. Process results for each statement using SQLMoreResults
    do {
        SQLSMALLINT num_cols;
        status = SQLNumResultCols(hstmt, &num_cols);
    
        if (num_cols > 0) {
            // This is a result-returning statement (e.g., SELECT)
            while (SQLFetch(hstmt) == SQL_SUCCESS) {
                // Process rows...
            }
        } else {
            // This is a non-result statement (e.g., CREATE, INSERT)
            SQLLEN row_count;
            SQLRowCount(hstmt, &row_count);
            // Process affected rows...
        }
    } while (SQLMoreResults(hstmt) == SQL_SUCCESS);

## Pricing

Querying through the ODBC driver for BigQuery is subject to standard BigQuery [analysis pricing](https://docs.cloud.google.com/bigquery/pricing#analysis) .
