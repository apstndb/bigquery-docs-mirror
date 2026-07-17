---
name: documents/docs.cloud.google.com/bigquery/docs/odbc-for-bigquery
uri: https://docs.cloud.google.com/bigquery/docs/odbc-for-bigquery
title: Use the ODBC driver for BigQuery
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

# Use the ODBC driver for BigQuery

> **Preview**
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

> **Note:** To request feedback or support for this feature, send an email to <bigquery-drivers-feedback@google.com> .

The Open Database Connectivity (ODBC) driver for BigQuery connects your non-Java applications to BigQuery, letting you use BigQuery features with your preferred tooling and infrastructure. To connect Java applications to BigQuery, use the [JDBC driver for BigQuery](https://docs.cloud.google.com/bigquery/docs/jdbc-for-bigquery) .

The ODBC driver for BigQuery is available under the [Apache 2.0 license](https://www.apache.org/licenses/LICENSE-2.0) .

## Before you begin

1.  Make sure that you're familiar with [ODBC drivers](https://learn.microsoft.com/en-us/sql/odbc/reference/what-is-odbc) and driver managers.

2.  Ensure that your operating system meets the following requirements:
    
    <table>
    <colgroup>
    <col style="width: 33%" />
    <col style="width: 33%" />
    <col style="width: 33%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th><strong>Operating system</strong></th>
    <th><strong>Supported architectures</strong></th>
    <th><strong>Minimum version and dependencies</strong></th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Windows</td>
    <td>32-bit (x86), 64-bit (x64)</td>
    <td>Version: Windows 10, Windows Server 2016 or later<br />
    <br />
    Dependency: Microsoft Visual C++ Redistributable for Visual Studio 2019 or 2022</td>
    </tr>
    <tr class="even">
    <td>macOS</td>
    <td>64-bit (x86_64), ARM64 (Apple Silicon)</td>
    <td>Version: macOS 12 (Monterey) or later<br />
    <br />
    Dependency: An ODBC driver manager (for example, <a href="https://www.unixodbc.org/">unixODBC</a> ). Ensure you add the installation directory to your <code dir="ltr" translate="no">DYLD_LIBRARY_PATH</code> .</td>
    </tr>
    <tr class="odd">
    <td>Linux</td>
    <td>64-bit (x86_64)</td>
    <td>Version: Any distribution with glibc 2.27 or later (for example, Ubuntu 20.04 LTS+, Debian 11+)<br />
    <br />
    Dependency: An ODBC Driver Manager (for example, <a href="https://www.unixodbc.org/">unixODBC</a> ). Ensure that you add the installation directory to your <code dir="ltr" translate="no">LD_LIBRARY_PATH</code> .</td>
    </tr>
    </tbody>
    </table>

3.  [Authenticate to BigQuery](https://docs.cloud.google.com/bigquery/docs/authentication) , and take note of the following information, which is used later when you establish a connection with the ODBC driver for BigQuery. You only need to note the information that corresponds to the authentication method that you use.
    
    **Authentication method**

## Install and configure the ODBC driver

You can install and configure the ODBC driver for BigQuery using either a Windows or non-Windows operating system.

### Windows

1.  Install the driver that corresponds to your application's architecture:
    
      - Download the [`ODBCDriverforBigQuery_windows_x86.msi` file](https://storage.googleapis.com/bq-driver-releases/odbc/ODBCDriverforBigQuery_windows_x86_latest.msi) for 32-bit applications.
      - Download the [`ODBCDriverforBigQuery_windows_x64.msi` file](https://storage.googleapis.com/bq-driver-releases/odbc/ODBCDriverforBigQuery_windows_x64_latest.msi) for 64-bit applications.

2.  Create a Data Source Name (DSN) by doing the following:
    
    1.  From the Windows **Start** menu, go to **ODBC Data Sources** , and select the version that has the same bitness as your client application.
    2.  On the **ODBC Data Source Administrator** page, click the **Drivers** tab.
    3.  In the list of installed ODBC drivers, locate **ODBC Driver for BigQuery** .
    4.  Select either the **System DSN** tab to create a DSN for all users or the **User DSN** tab to create a DSN for the current user. System DSNs are generally recommended because some applications load data using different user accounts and might not detect other User DSNs.
    5.  Click **Add** .
    6.  In the **Create New Data Source** dialog, select **ODBC Driver for BigQuery** , and then click **Finish** . The **ODBC Driver for BigQuery DSN Setup** dialog opens.
    7.  In the **Data Source Name** field, enter a name for your DSN.
    8.  Add connection properties. For a full list of properties, see [Connection properties](https://docs.cloud.google.com/bigquery/docs/odbc-for-bigquery#connection_properties) .

### Non-Windows

1.  Install the driver that corresponds to your operating system:
    
      - Download the [`ODBCDriverforBigQuery_linux_latest.zip` file](https://storage.googleapis.com/bq-driver-releases/odbc/ODBCDriverforBigQuery_linux_latest.zip) for Linux.
      - Download the [`ODBCDriverforBigQuery_macos_latest.tar.gz` file](https://storage.googleapis.com/bq-driver-releases/odbc/ODBCDriverforBigQuery_macos_latest.tar.gz) for macOS.

2.  Extract the contents of the downloaded ZIP or TAR file.

3.  Move the contents of the ZIP or TAR file to the directory where you want to install the connector. The ODBC driver for BigQuery shared object path is `  INSTALL_DIR /lib/libgoogle_cloud_odbc_bq_driver.so ` , where `  INSTALL_DIR  ` is your installation directory.

4.  Update your `.ini` files to reflect the new path of the connector.
    
    The following example updates the `.ini` files in a Linux system:
    
        unzip linux_odbc-driver.VERSION.zip -d linux_odbc-driver.VERSION/
        cd ./linux_odbc-driver.VERSION
        export INSTALL_DIR=$(pwd)
        export ODBCINI=$INSTALL_DIR/odbc.ini
        export ODBCINSTINI=$INSTALL_DIR/odbcinst.ini
        export GOOGLEBIGQUERYODBCINI=$INSTALL_DIR/googlebigqueryodbc.ini
    
    Replace `  VERSION  ` with the driver version.

## Establish a connection

To establish a connection between your application and BigQuery with the ODBC driver for BigQuery, identify your connection string. You can skip this step if you already configured connection properties through your DSN.

The connection string has the following format:

    Driver=ODBC Driver for BigQuery;ProjectId=PROJECT_ID;OAuthType=AUTH_TYPE;AUTH_PROPS;OTHER_PROPS

Replace the following:

  - `PROJECT_ID` : the ID of your BigQuery project.
  - `AUTH_TYPE` : a number specifying the type of authentication that you used. Select one of the following:
      - `0` : for service account authentication
      - `3` : for Application Default Credential authentication
      - `4` : for Workload Identity Federation or Workforce Identity Federation authentication
  - `AUTH_PROPS` : the authentication information that you noted when you [authenticated to BigQuery](https://docs.cloud.google.com/bigquery/docs/odbc-for-bigquery#before_you_begin) , listed in the `property_1=value_1; property_2=value_2;...` format—for example, `KeyFilePath=my-sa-key` , if you authenticated with a service account.
  - `OTHER_PROPS` (optional): additional connection properties for the ODBC driver, listed in the `property_1=value_1; property_2=value_2;...` format. For a full list of connection properties, see [Connection properties](https://docs.cloud.google.com/bigquery/docs/odbc-for-bigquery#connection_properties) .

### Connection properties

ODBC driver connection properties are configuration parameters that you include in the connection string when you [establish a connection](https://docs.cloud.google.com/bigquery/docs/odbc-for-bigquery#establish_a_connection) to a database. The ODBC driver for BigQuery supports the following connection properties.

> **Note:** All connection property names are case-insensitive. Boolean connection properties accept both `TRUE` / `FALSE` and `1` / `0` .

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
<td>Determines whether the driver can use the BigQuery Storage Read API.</td>
<td><code dir="ltr" translate="no">0</code></td>
<td>Boolean</td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">AllowLargeResults</code></td>
<td>Determines if the driver processes query results that are larger than 128 MB when the <code dir="ltr" translate="no">QueryDialect</code> property is set to <code dir="ltr" translate="no">BIG_QUERY</code> . If the <code dir="ltr" translate="no">QueryDialect</code> property is set to <code dir="ltr" translate="no">SQL</code> , the driver always processes large query results.</td>
<td><code dir="ltr" translate="no">0</code></td>
<td>Boolean</td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">BYOID_AudienceUrl</code></td>
<td>Contains the resource name for the Workload Identity Pool or the Workforce Pool and the provider identifier in that pool.</td>
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
<td>Set the project when it is a Workforce Pool and not a Workload Identity Pool.</td>
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
<td>Determines the scope of metadata that table or column metadata methods return. When false, no filtering occurs. You must also set the <code dir="ltr" translate="no">DefaultDataset</code> property to enable filtering.</td>
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
<li><code dir="ltr" translate="no">1</code> : The driver creates jobs for every query ( <code dir="ltr" translate="no">JOB_CREATION_REQUIRED</code> )</li>
<li><code dir="ltr" translate="no">2</code> : The driver executes queries without jobs ( <code dir="ltr" translate="no">JOB_CREATION_OPTIONAL</code> )</li>
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
<td>Specifies the name of the KMS key to use when encrypting and decrypting data.</td>
<td>N/A</td>
<td>String</td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">LargeResultsDataSetId</code></td>
<td>Specifies the destination dataset for storing large query results.</td>
<td>N/A</td>
<td>String</td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">LargeResultsDatasetExpirationTime</code></td>
<td>Specifies the lifetime of all tables in the large results dataset, in milliseconds.</td>
<td><code dir="ltr" translate="no">3600000</code></td>
<td>Long</td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">Location</code></td>
<td>Specifies the location where the driver creates or queries datasets.</td>
<td>N/A</td>
<td>String</td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">LogLevel</code></td>
<td>Limits the detail that the driver logs during interactions. For more information, see <a href="https://docs.cloud.google.com/bigquery/docs/odbc-for-bigquery#logging">Logging</a> . Choose one of the following:<br />

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
<td>Specifies the directory where the driver writes log files. For more information, see <a href="https://docs.cloud.google.com/bigquery/docs/odbc-for-bigquery#logging">Logging</a> .</td>
<td>N/A</td>
<td>String</td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">LogFileCount</code></td>
<td>Specifies the maximum number of log files to keep.</td>
<td><code dir="ltr" translate="no">0</code></td>
<td>Integer</td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">LogFileSize</code></td>
<td>Specifies the maximum size of each log file in KB.</td>
<td><code dir="ltr" translate="no">0</code></td>
<td>Long</td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">MaxResults</code></td>
<td>Specifies the number of results per page in the BigQuery API result.</td>
<td><code dir="ltr" translate="no">10000</code></td>
<td>Long</td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">MaxThreads</code></td>
<td>Defines the maximum number of threads that the connector can use for concurrent processing in a thread pool. To configure this property as a connector-wide setting for non-Windows connectors, specify it in the <code dir="ltr" translate="no">googlebigqueryodbc.ini</code> file.</td>
<td><code dir="ltr" translate="no">8</code></td>
<td>Integer</td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">OAuthMechanism</code></td>
<td>The authentication type. Choose one of the following:<br />

<ul>
<li><code dir="ltr" translate="no">0</code> : Service account authentication</li>
<li><code dir="ltr" translate="no">3</code> : Application Default Credential authentication</li>
<li><code dir="ltr" translate="no">4</code> : Workload Identity Federation or Workforce Identity Federation authentication</li>
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
<td>Custom endpoints to overwrite default endpoints. Examples:<br />

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
<td>Enables the query caching feature in BigQuery.</td>
<td><code dir="ltr" translate="no">true</code></td>
<td>Boolean</td>
<td>No</td>
</tr>
</tbody>
</table>

## Data type mapping

When you run queries through the ODBC driver for BigQuery, the following data type mapping occurs:

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

## Logging

To enable logging with the driver, do the following:

### Windows

Configure logging using the DSN configuration dialog in the ODBC Data Source Administrator.

### Non-Windows

1.  Create or edit a configuration file, such as `google.bigqueryodbc.ini` , and add the logging options under the `[Driver]` section. The following is an example:
    
        [Driver]
        LogLevel=3
        LogPath=/path/to/log/directory
        LogFileCount=200
        LogFileSize=1000

2.  Set the `GOOGLEBIGQUERYODBCINI` environment variable to the path of this file:
    
        export GOOGLEBIGQUERYODBCINI=/path/to/google.bigqueryodbc.ini

> **Note:** You might need to restart your application for the changes to take effect.

The driver supports logging levels 0 to 3. We recommend starting with `LogLevel=3` (INFO) for troubleshooting.

| ODBC logging level | Description                                                            |
| ------------------ | ---------------------------------------------------------------------- |
| 0 (OFF)            | Disables all logging.                                                  |
| 1 (ERROR)          | Logs error events.                                                     |
| 2 (WARNING)        | Logs warning events.                                                   |
| 3 (INFO)           | Logs general information that describes the progress of the connector. |

## Examples

The following examples demonstrate how to use parameterized queries and multi-statement scripts with the ODBC driver.

**Parameterized queries**

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

**Multi-statement scripts**

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

You can download the ODBC driver for BigQuery at no cost. However, when you use the driver, [standard BigQuery analysis pricing](https://cloud.google.com/bigquery/pricing#analysis) applies.

## What's next

  - Learn more about the [JDBC driver for BigQuery](https://docs.cloud.google.com/bigquery/docs/jdbc-for-bigquery) .
  - Explore other [BigQuery developer tools](https://docs.cloud.google.com/bigquery/docs/developer-overview) .
