---
name: documents/docs.cloud.google.com/bigquery/docs/jdbc-for-bigquery
uri: https://docs.cloud.google.com/bigquery/docs/jdbc-for-bigquery
title: Use the JDBC driver for BigQuery
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

# Use the JDBC driver for BigQuery

The Java Database Connectivity (JDBC) driver for BigQuery connects your Java applications to BigQuery, letting you use BigQuery features with your preferred tooling and infrastructure. To connect non-Java applications to BigQuery, use the [Open Database Connectivity (ODBC) driver for BigQuery](https://docs.cloud.google.com/bigquery/docs/odbc-for-bigquery) .

## Limitations

The JDBC driver for BigQuery is subject to the following limitations:

  - The driver is specific to BigQuery and can't be used with other products or services.
  - The `INTERVAL` data type isn't supported with the BigQuery Storage Read API.
  - All [data manipulation language (DML) limitations](https://docs.cloud.google.com/bigquery/docs/data-manipulation-language#dml-limitations) apply.

## Before you begin

1.  Make sure that you're familiar with JDBC drivers, Apache Maven, and the [`java.sql` package](https://docs.oracle.com/javase/8/docs/api/java/sql/package-summary.html) .

2.  Verify that your system is configured with Java Runtime Environment (JRE) 8.0 or later. For information on checking your JRE version, see [Verifying the JRE Environment](https://docs.oracle.com/goldengate/dir1212/gg-director/GDRAD/verifying-jre-environment.htm) .

3.  [Authenticate to BigQuery](https://docs.cloud.google.com/bigquery/docs/authentication) , and take note of the following information, which is used later when you establish a connection with the JDBC driver for BigQuery. You only need to note the information that corresponds to the authentication method that you use.
    
    **Authentication method**

## Install and configure the JDBC driver

You can install and configure the JDBC driver for BigQuery by either direcly downloading the uber-JAR file or by using Maven.

### Direct download configuration

To configure the JDBC driver through direct download, do the following:

1.  Download the [1.2.0 version of the driver](https://storage.googleapis.com/bq-driver-releases/jdbc/google-cloud-bigquery-jdbc-1.2.0-all.jar) .
2.  Copy the downloaded file to the location specified by your software.

For information on feature changes and workflow updates, see [the changelog](https://github.com/googleapis/google-cloud-java/blob/main/java-bigquery-jdbc/CHANGELOG.md) .

### Previous JDBC driver for BigQuery versions

  - [1.1.0](https://storage.googleapis.com/bq-driver-releases/jdbc/google-cloud-bigquery-jdbc-1.1.0-all.jar)
  - [1.0.0](https://storage.googleapis.com/bq-driver-releases/jdbc/google-cloud-bigquery-jdbc-1.0.0-all.jar)

### Maven configuration

The JDBC driver for BigQuery is available on [Maven Central](https://mvnrepository.com/artifact/com.google.cloud/google-cloud-bigquery-jdbc) .

To configure your development environment with the JDBC driver, add the driver as a dependency to your project:

### Maven

Add the following dependency to your `pom.xml` file:

    <dependency>
        <groupId>com.google.cloud</groupId>
        <artifactId>google-cloud-bigquery-jdbc</artifactId>
        <version>1.1.0</version>
    </dependency>

### Maven using uber-JAR

Add the following dependency to your `pom.xml` file:

    <dependency>
        <groupId>com.google.cloud</groupId>
        <artifactId>google-cloud-bigquery-jdbc</artifactId>
        <version>1.1.0</version>
        <classifier>all</classifier>
        <exclusions>
          <exclusion>
            <groupId>*</groupId>
            <artifactId>*</artifactId>
          </exclusion>
        </exclusions>
    </dependency>

### Gradle

Add the following to your `build.gradle` file:

    dependencies {
    // ... other dependencies
    implementation("com.google.cloud:google-cloud-bigquery-jdbc:1.1.0")
    }

## Establish a connection

To establish a connection between your Java application and BigQuery with the JDBC driver for BigQuery, do the following:

1.  Identify your connection string for the JDBC driver for BigQuery. This string captures all the required information to establish a connection between your Java application and BigQuery. The connection string has the following format:
    
        jdbc:bigquery://HOST:PORT;ProjectId=PROJECT_ID;OAuthType=AUTH_TYPE;AUTH_PROPS;OTHER_PROPS
    
    Replace the following:
    
      - `HOST` : the DNS or IP address of the server.
      - `PORT` : the TCP port number.
      - `PROJECT_ID` : the ID of your BigQuery project.
      - `AUTH_TYPE` : a number specifying the type of authentication that you used. One of the following:
          - `0` : for service account authentication (standard and key file)
          - `1` : for Google user account authentication
          - `2` : for pre-generated refresh or access token authentication
          - `3` : for Application Default Credential authentication
          - `4` : for other authentication methods
      - `AUTH_PROPS` : the authentication information that you noted when you [authenticated to BigQuery](https://docs.cloud.google.com/bigquery/docs/jdbc-for-bigquery#before_you_begin) , listed in the `property_1=value_1; property_2=value_2;...` format—for example, `OAuthPvtKeyPath=path/to/file/secret.json` , if you authenticated with a service account key file.
      - `OTHER_PROPS` (optional): additional connection properties for the JDBC driver, listed in the `property_1=value_1; property_2=value_2;...` format. For a full list of connection properties, see [Connection properties](https://docs.cloud.google.com/bigquery/docs/jdbc-for-bigquery#connection_properties) .

2.  Connect your Java application to the JDBC driver for BigQuery with either the [`DriverManager`](https://docs.oracle.com/javase/8/docs/api/java/sql/DriverManager.html) or [`DataSource`](https://docs.oracle.com/javase/8/docs/api/javax/sql/DataSource.html) class.
    
      - Connect with the `DriverManager` class:
        
            import java.sql.Connection;
            import java.sql.DriverManager;
            
            private static Connection getJdbcConnectionDM(){
              Connection connection = DriverManager.getConnection(CONNECTION_STRING);
              return connection;
            }
        
        Replace `CONNECTION_STRING` with the connection string from the previous step.
    
      - Connect with the `DataSource` class:
        
            import com.google.cloud.bigquery.jdbc.DataSource;
            import java.sql.Connection;
            import java.sql.SQLException;
            
            private static public Connection getJdbcConnectionDS() throws SQLException {
              Connection connection = null;
              DataSource dataSource = new com.google.cloud.bigquery.jdbc.DataSource();
              dataSource.setURL(CONNECTION_STRING);
              connection = dataSource.getConnection();
              return connection;
            }
        
        Replace `CONNECTION_STRING` with the connection string from the previous step.
        
        The `DataSource` class also has setter methods that you can use to set [connection properties](https://docs.cloud.google.com/bigquery/docs/jdbc-for-bigquery#connection_properties) , rather than including them in the connection string. The following is an example:
        
            private static Connection getConnection() throws SQLException {
              DataSource ds = new DataSource();
              ds.setURL(jdbc:bigquery://https://www.googleapis.com/bigquery/v2:443;);
              ds.setAuthType(3);  // Application Default Credentials
              ds.setProjectId("MyTestProject");
              ds.setEnableHighThroughputAPI(true);
              ds.setLogLevel("6");
              ds.setUseQueryCache(false);
              return ds.getConnection();
            }

### Connection properties

JDBC driver connection properties are configuration parameters that you include in the connection string or pass through setter methods when you [establish a connection](https://docs.cloud.google.com/bigquery/docs/jdbc-for-bigquery#establish_a_connection) to a database. The following connection properties are supported by the JDBC driver for BigQuery.

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
<td><code dir="ltr" translate="no">AllowLargeResults</code></td>
<td>Determines if the driver processes query results that are larger than 128 MB when the <code dir="ltr" translate="no">QueryDialect</code> property is set to <code dir="ltr" translate="no">BIG_QUERY</code> . If the <code dir="ltr" translate="no">QueryDialect</code> property is set to <code dir="ltr" translate="no">SQL</code> , the driver always processes large query results.</td>
<td><code dir="ltr" translate="no">TRUE</code></td>
<td>Boolean</td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">BYOID_AudienceUri</code></td>
<td>The audience property in an external account configuration file. The audience property can contain the resource name for the workload identity pool or workforce pool, as well as the provider identifier in that pool.</td>
<td>N/A</td>
<td>String</td>
<td>Only when <code dir="ltr" translate="no">OAuthType=4</code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">BYOID_CredentialSource</code></td>
<td>The token retrieval and environmental information.</td>
<td>N/A</td>
<td>String</td>
<td>Only when <code dir="ltr" translate="no">OAuthType=4</code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">BYOID_PoolUserProject</code></td>
<td>The user project when a workforce pool is being used for authentication.</td>
<td>N/A</td>
<td>String</td>
<td>Only when <code dir="ltr" translate="no">OAuthType=4</code> and using the workforce pool</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">BYOID_SA_Impersonation_Uri</code></td>
<td>The URI for the service account impersonation when a workforce pool is being used for authentication.</td>
<td>N/A</td>
<td>String</td>
<td>Only when <code dir="ltr" translate="no">OAuthType=4</code> and using the workforce pool</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">BYOID_SubjectTokenType</code></td>
<td>The Security Token Service token based on the token exchange specification. One of the following:<br />

<ul>
<li><code dir="ltr" translate="no">urn:ietf:params:oauth:token-type:jwt</code></li>
<li><code dir="ltr" translate="no">urn:ietf:params:oauth:token-type:id_token</code></li>
<li><code dir="ltr" translate="no">urn:ietf:params:oauth:token-type:saml2</code></li>
<li><code dir="ltr" translate="no">urn:ietf:params:aws:token-type:aws4_request</code></li>
</ul></td>
<td><code dir="ltr" translate="no">urn:ietf:params:oauth:tokentype:id_token</code></td>
<td>String</td>
<td>Only when <code dir="ltr" translate="no">OAuthType=4</code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">BYOID_TokenUri</code></td>
<td>The Security Token Service token exchange endpoint.</td>
<td><code dir="ltr" translate="no">https://sts.googleapis.com/v1/token</code></td>
<td>String</td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">ConnectionPoolSize</code></td>
<td>The connection pool size, if connection pooling is enabled.</td>
<td><code dir="ltr" translate="no">10</code></td>
<td>Long</td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">DefaultDataset</code></td>
<td>The dataset that's used when one isn't specified in a query.</td>
<td>N/A</td>
<td>String</td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">EnableGcpLogExporter</code></td>
<td>Determines if the driver automatically exports logs to Cloud Logging (if no custom or global OpenTelemetry instance is used). For more information, see <a href="https://docs.cloud.google.com/bigquery/docs/jdbc-for-bigquery#opentelemetry">OpenTelemetry</a> .</td>
<td><code dir="ltr" translate="no">FALSE</code></td>
<td>Boolean</td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">EnableGcpTraceExporter</code></td>
<td>Determines if the driver automatically exports traces to Cloud Trace (if no custom or global OpenTelemetry instance is used). For more information, see <a href="https://docs.cloud.google.com/bigquery/docs/jdbc-for-bigquery#opentelemetry">OpenTelemetry</a> .</td>
<td><code dir="ltr" translate="no">FALSE</code></td>
<td>Boolean</td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">EnableHighThroughputAPI</code></td>
<td>Determines if the Storage Read API can be used. The <code dir="ltr" translate="no">HighThroughputActivationRatio</code> and <code dir="ltr" translate="no">HighThroughputMinTableSize</code> properties must also be set to <code dir="ltr" translate="no">TRUE</code> to use the Storage Read API.</td>
<td><code dir="ltr" translate="no">FALSE</code></td>
<td>Boolean</td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">EnableProjectDiscovery</code></td>
<td>Determines if database metadata methods discover datasets across all accessible Google Cloud projects. When set to <code dir="ltr" translate="no">FALSE</code> , discovery is restricted to the default <code dir="ltr" translate="no">ProjectId</code> .</td>
<td><code dir="ltr" translate="no">FALSE</code></td>
<td>Boolean</td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">EnableSession</code></td>
<td>Determines if the connection starts a session. If set to <code dir="ltr" translate="no">TRUE</code> , the session ID is passed to all subsequent queries.</td>
<td><code dir="ltr" translate="no">FALSE</code></td>
<td>Boolean</td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">EnableWriteAPI</code></td>
<td>Determines if the Storage Write API (gRPC) can be used. It must be set to <code dir="ltr" translate="no">TRUE</code> to enable bulk inserts.</td>
<td><code dir="ltr" translate="no">FALSE</code></td>
<td>Boolean</td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">EndpointOverrides</code></td>
<td>Custom endpoints to overwrite the following:<br />

<ul>
<li><code dir="ltr" translate="no">BIGQUERY=https://bigquery.googleapis.com</code></li>
<li><code dir="ltr" translate="no">READ_API=https://bigquerystorage.googleapis.com</code></li>
<li><code dir="ltr" translate="no">OAUTH2=https://oauth2.googleapis.com</code></li>
<li><code dir="ltr" translate="no">STS=https://sts.googleapis.com</code></li>
</ul></td>
<td>N/A</td>
<td>Comma-separated string</td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">FilterTablesOnDefaultDataset</code></td>
<td>Determines the scope of metadata returned by the <code dir="ltr" translate="no">DatabaseMetaData.getTables()</code> and <code dir="ltr" translate="no">DatabaseMetaData.getColumns()</code> methods. When set to <code dir="ltr" translate="no">FALSE</code> , no filtering occurs. The <code dir="ltr" translate="no">DefaultDataset</code> property must also be set to enable filtering.</td>
<td><code dir="ltr" translate="no">FALSE</code></td>
<td>Boolean</td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">GcpTelemetryCredentials</code></td>
<td>The credentials used to authenticate telemetry exporters. Accepts a path to a service account JSON key or the raw JSON string. Defaults to connection credentials if not set. For more information, see <a href="https://docs.cloud.google.com/bigquery/docs/jdbc-for-bigquery#opentelemetry">OpenTelemetry</a> .</td>
<td>N/A</td>
<td>String</td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">GcpTelemetryProjectId</code></td>
<td>The destination Google Cloud project ID for telemetry. Defaults to the primary <code dir="ltr" translate="no">ProjectId</code> . For more information, see <a href="https://docs.cloud.google.com/bigquery/docs/jdbc-for-bigquery#opentelemetry">OpenTelemetry</a> .</td>
<td>N/A</td>
<td>String</td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">HighThroughputActivationRatio</code></td>
<td>The threshold for the number of pages in a query response. When this number is exceeded, and the <code dir="ltr" translate="no">EnableHighThroughputAPI</code> and <code dir="ltr" translate="no">HighThroughputMinTableSize</code> conditions are met, the driver starts using the Storage Read API.</td>
<td><code dir="ltr" translate="no">2</code></td>
<td>Integer</td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">HighThroughputMinTableSize</code></td>
<td>The threshold for the number of rows in a query response. When this number is exceeded, and the <code dir="ltr" translate="no">EnableHighThroughputAPI</code> and <code dir="ltr" translate="no">HighThroughputActivationRatio</code> conditions are met, the driver starts using the Storage Read API.</td>
<td><code dir="ltr" translate="no">10000</code></td>
<td>Integer</td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">JobCreationMode</code></td>
<td>Determines if queries are run with or without jobs. A <code dir="ltr" translate="no">1</code> value means that jobs are created for every query, and a <code dir="ltr" translate="no">2</code> value means that queries can be executed without jobs.</td>
<td><code dir="ltr" translate="no">2</code></td>
<td>Integer</td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">JobTimeout</code></td>
<td>The job timeout (in seconds) after which the job is cancelled on the server.</td>
<td><code dir="ltr" translate="no">0</code></td>
<td>Long</td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">KMSKeyName</code></td>
<td>The KMS key name for encrypting data.</td>
<td>N/A</td>
<td>String</td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">Labels</code></td>
<td>Labels that are associated with the query to organize and group query jobs.</td>
<td>N/A</td>
<td>Map&lt;String, String&gt;</td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">LargeResultDataset</code></td>
<td>The destination dataset for large query results, only when the <code dir="ltr" translate="no">LargeResultTable</code> property is set. When you set this property, data writes bypass the result cache and trigger billing for each query, even if the results are small.</td>
<td><code dir="ltr" translate="no">_google_jdbc</code></td>
<td>String</td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">LargeResultsDatasetExpirationTime</code></td>
<td>The lifetime of all tables in a large result dataset, in milliseconds. This property is ignored if the dataset already has a default expiration time set.</td>
<td><code dir="ltr" translate="no">3600000</code></td>
<td>Long</td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">LargeResultTable</code></td>
<td>The destination table for large query results, only when the <code dir="ltr" translate="no">LargeResultDataset</code> property is set. When you set this property, data writes bypass the result cache and trigger billing for each query, even if the results are small.</td>
<td><code dir="ltr" translate="no">temp_table...</code></td>
<td>String</td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">ListenerPoolSize</code></td>
<td>The listener pool size, if connection pooling is enabled.</td>
<td><code dir="ltr" translate="no">10</code></td>
<td>Long</td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">Location</code></td>
<td>The <a href="https://docs.cloud.google.com/bigquery/docs/locations">location</a> where datasets are created or queried. BigQuery automatically determines the location if this property isn't set.</td>
<td>N/A</td>
<td>String</td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">LogLevel</code></td>
<td>The level of detail logged by the driver. For more information, see <a href="https://docs.cloud.google.com/bigquery/docs/jdbc-for-bigquery#logging">Logging</a> .</td>
<td><code dir="ltr" translate="no">0</code></td>
<td>Integer</td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">LogPath</code></td>
<td>The directory where log files are written.</td>
<td>N/A</td>
<td>String</td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">MaximumBytesBilled</code></td>
<td>The limit of bytes billed. Queries with bytes billed greater than this number fail without incurring a charge.</td>
<td><code dir="ltr" translate="no">0</code></td>
<td>Long</td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">MaxResults</code></td>
<td>The maximum number of results per page.</td>
<td><code dir="ltr" translate="no">10000</code></td>
<td>Long</td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">MetaDataFetchThreadCount</code></td>
<td>The number of threads used for database metadata methods.</td>
<td><code dir="ltr" translate="no">32</code></td>
<td>Integer</td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">OAuthAccessToken</code></td>
<td>The access token that's used for pre-generated access token authentication.</td>
<td>N/A</td>
<td>String</td>
<td>Only when <code dir="ltr" translate="no">OAUTH_TYPE=2</code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">OAuthClientId</code></td>
<td>The client ID for pre-generated refresh token authentication and user account authentication.</td>
<td>N/A</td>
<td>String</td>
<td>Only when <code dir="ltr" translate="no">OAUTH_TYPE=1</code> or <code dir="ltr" translate="no">OAUTH_TYPE=2</code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">OAuthClientSecret</code></td>
<td>The client secret for pre-generated refresh token authentication and user account authentication.</td>
<td>N/A</td>
<td>String</td>
<td>Only when <code dir="ltr" translate="no">OAUTH_TYPE=1</code> or <code dir="ltr" translate="no">OAUTH_TYPE=2</code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">OAuthP12Password</code></td>
<td>The password for the PKCS12 key file.</td>
<td><code dir="ltr" translate="no">notasecret</code></td>
<td>String</td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">OAuthPvtKey</code></td>
<td>The service account key when using service account authentication. This value can be a raw JSON keyfile object or a path to the JSON keyfile.</td>
<td>N/A</td>
<td>String</td>
<td>Only when <code dir="ltr" translate="no">OAUTH_TYPE=0</code> and the <code dir="ltr" translate="no">OAuthPvtKeyPath</code> value isn't set</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">OAuthPvtKeyPath</code></td>
<td>The path to the service account key when using service account authentication.</td>
<td>N/A</td>
<td>String</td>
<td>Only when <code dir="ltr" translate="no">OAUTH_TYPE=0</code> and the <code dir="ltr" translate="no">OAuthPvtKey</code> and <code dir="ltr" translate="no">OAuthServiceAcctEmail</code> values aren't set</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">OAuthRefreshToken</code></td>
<td>The refresh token for pre-generated refresh token authentication.</td>
<td>N/A</td>
<td>String</td>
<td>Only when <code dir="ltr" translate="no">OAUTH_TYPE=2</code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">OAuthServiceAcctEmail</code></td>
<td>The service account email when using service account authentication.</td>
<td>N/A</td>
<td>String</td>
<td>Only when <code dir="ltr" translate="no">OAUTH_TYPE=0</code> and the <code dir="ltr" translate="no">OAuthPvtKeyPath</code> value isn't set</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">OAuthType</code></td>
<td>The authentication type. One of the following:<br />

<ul>
<li><code dir="ltr" translate="no">0</code> : service account authentication</li>
<li><code dir="ltr" translate="no">1</code> : user account authentication</li>
<li><code dir="ltr" translate="no">2</code> : pre-generated refresh or access token authentication</li>
<li><code dir="ltr" translate="no">3</code> : Application Default Credential authentication</li>
<li><code dir="ltr" translate="no">4</code> : other authentication methods</li>
</ul></td>
<td><code dir="ltr" translate="no">-1</code></td>
<td>Integer</td>
<td>Yes</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">PartnerToken</code></td>
<td>A token that's used by Google Cloud partners to track usage of the driver.</td>
<td>N/A</td>
<td>String</td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">ProjectId</code></td>
<td>The default project ID for the driver. This project is used to execute queries and is billed for resource usage. If not set, the driver infers a project ID.</td>
<td>N/A</td>
<td>String</td>
<td>No, but highly recommended</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">ProxyHost</code></td>
<td>The hostname or IP address of a proxy server through which the JDBC connection is routed.</td>
<td>N/A</td>
<td>String</td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">ProxyPort</code></td>
<td>The port number on which the proxy server is listening for connections.</td>
<td>N/A</td>
<td>String</td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">ProxyPwd</code></td>
<td>The password for authentication when connecting through a proxy server that requires it.</td>
<td>N/A</td>
<td>String</td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">ProxyUid</code></td>
<td>The username for authentication when connecting through a proxy server that requires it.</td>
<td>N/A</td>
<td>String</td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">QueryDialect</code></td>
<td>The SQL dialect for query execution. Use <code dir="ltr" translate="no">SQL</code> for GoogleSQL (highly recommended) and <code dir="ltr" translate="no">BIG_QUERY</code> for legacy SQL.</td>
<td><code dir="ltr" translate="no">SQL</code></td>
<td>String</td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">QueryProperties</code></td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/ConnectionProperty">REST connection properties</a> that customize query behavior.</td>
<td>N/A</td>
<td>Map&lt;String, String&gt;</td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">RequestGoogleDriveScope</code></td>
<td>Adds read-only Drive scope to the connection when set to <code dir="ltr" translate="no">1</code> .</td>
<td><code dir="ltr" translate="no">0</code></td>
<td>Integer</td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">RetryInitialDelay</code></td>
<td>Sets the delay (in seconds) before the first retry.</td>
<td><code dir="ltr" translate="no">0</code></td>
<td>Long</td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">RetryMaxDelay</code></td>
<td>Sets the maximum limit (in seconds) for the retry delay.</td>
<td><code dir="ltr" translate="no">0</code></td>
<td>Long</td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">ServiceAccountImpersonationChain</code></td>
<td>A comma-separated list of service account emails in the impersonation chain.</td>
<td>N/A</td>
<td>String</td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">ServiceAccountImpersonationEmail</code></td>
<td>The service account email to be impersonated.</td>
<td>N/A</td>
<td>String</td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">ServiceAccountImpersonationScopes</code></td>
<td>A comma-separated list of OAuth2 scopes to use with the impersonated account.</td>
<td><code dir="ltr" translate="no">https://www.googleapis.com/auth/bigquery</code></td>
<td>String</td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">ServiceAccountImpersonationTokenLifetime</code></td>
<td>The impersonated account token lifetime (in seconds).</td>
<td><code dir="ltr" translate="no">3600</code></td>
<td>Integer</td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">SSLTrustStore</code></td>
<td>The full path to the Java TrustStore that contains trusted Certificate Authority (CA) certificates. The driver utilizes this truststore to validate the identity of the server during the SSL/TLS handshake.</td>
<td>N/A</td>
<td>String</td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">SSLTrustStoreProvider</code></td>
<td>The Java Cryptography Extension (JCE) provider used for the <code dir="ltr" translate="no">SSLTrustStore</code> property.</td>
<td>N/A</td>
<td>String</td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">SSLTrustStorePwd</code></td>
<td>The password to the Java TrustStore specified in the <code dir="ltr" translate="no">SSLTrustStore</code> property.</td>
<td>N/A</td>
<td>String</td>
<td>Only if the Java TrustStore is password-protected</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">SSLTrustStoreType</code></td>
<td>The format of the truststore file specified in the <code dir="ltr" translate="no">SSLTrustStore</code> property (such as <code dir="ltr" translate="no">JKS</code> , <code dir="ltr" translate="no">PKCS12</code> , or <code dir="ltr" translate="no">ROTKS</code> ).</td>
<td>N/A</td>
<td>String</td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">SWA_ActivationRowCount</code></td>
<td>The threshold of <code dir="ltr" translate="no">executeBatch insert</code> rows which, when exceeded, causes the connector to switch to the Storage Write API (gRPC).</td>
<td><code dir="ltr" translate="no">3</code></td>
<td>Integer</td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">SWA_AppendRowCount</code></td>
<td>The size of the write stream.</td>
<td><code dir="ltr" translate="no">1000</code></td>
<td>Integer</td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">Timeout</code></td>
<td>The length of time, in seconds, that the connector retries a failed API call before timing out.</td>
<td><code dir="ltr" translate="no">0</code></td>
<td>Long</td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">UniverseDomain</code></td>
<td>The top-level domain that's associated with your organization's Google Cloud resources.</td>
<td><code dir="ltr" translate="no">googleapis.com</code></td>
<td>String</td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">UnsupportedHTAPIFallback</code></td>
<td>Determines if the connector falls back to the REST API (when set to <code dir="ltr" translate="no">TRUE</code> ) or returns an error (when set to <code dir="ltr" translate="no">FALSE</code> ).</td>
<td><code dir="ltr" translate="no">TRUE</code></td>
<td>Boolean</td>
<td>No</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">UseGlobalOpenTelemetry</code></td>
<td>Determines if the driver uses <code dir="ltr" translate="no">GlobalOpenTelemetry.get()</code> for instrumentation. For more information, see <a href="https://docs.cloud.google.com/bigquery/docs/jdbc-for-bigquery#opentelemetry">OpenTelemetry</a> .</td>
<td><code dir="ltr" translate="no">FALSE</code></td>
<td>Boolean</td>
<td>No</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">UseQueryCache</code></td>
<td>Enables query caching.</td>
<td><code dir="ltr" translate="no">TRUE</code></td>
<td>Boolean</td>
<td>No</td>
</tr>
</tbody>
</table>

## Run queries with the driver

With your Java application connected to BigQuery through the JDBC driver, you can now run queries in your development environment through the [standard JDBC process](https://docs.oracle.com/javase/tutorial/jdbc/basics/processingsqlstatements.html) . All [BigQuery quotas and limits](https://docs.cloud.google.com/bigquery/quotas) apply.

### Data type mapping

When you run queries through the JDBC driver for BigQuery, the following data type mapping occurs:

| **GoogleSQL type** | **Java type** |
| ------------------ | ------------- |
| `ARRAY`            | `Array`       |
| `BIGNUMERIC`       | `BigDecimal`  |
| `BOOL`             | `Boolean`     |
| `BYTES`            | `byte[]`      |
| `DATE`             | `Date`        |
| `DATETIME`         | `String`      |
| `FLOAT64`          | `Double`      |
| `GEOGRAPHY`        | `String`      |
| `INT64`            | `Long`        |
| `INTERVAL`         | `String`      |
| `JSON`             | `String`      |
| `NUMERIC`          | `BigDecimal`  |
| `STRING`           | `String`      |
| `STRUCT`           | `Struct`      |
| `TIME`             | `Time`        |
| `TIMESTAMP`        | `Timestamp`   |

### Examples

The following sections provide examples that use BigQuery features through the JDBC driver for BigQuery.

#### Positional parameters

The following example runs a query with a [positional parameter](https://docs.cloud.google.com/bigquery/docs/parameterized-queries) :

    PreparedStatement preparedStatement = connection.prepareStatement(
        "SELECT * FROM MyTestTable where testColumn = ?");
    preparedStatement.setString(1, "string2");
    ResultSet resultSet = statement.executeQuery(selectQuery);

#### Nested and repeated records

The following example queries the base record of `Struct` data:

    ResultSet resultSet = statement.executeQuery("SELECT STRUCT(\"Adam\" as name, 5 as age)");
        resultSet.next();
        Struct obj = (Struct) resultSet.getObject(1);
        System.out.println(obj.toString());

The driver returns the base record as a struct object or a string representation of a JSON object. The result is similar to the following:

    {
      "v": {
        "f": [
          {
            "v": "Adam"
          },
          {
            "v": "5"
          }
        ]
      }
    }

The following example queries the subcomponents of a `Struct` object:

    ResultSet resultSet = statement.executeQuery("SELECT STRUCT(\"Adam\" as name, 5 as age)");
        resultSet.next();
        Struct structObject = (Struct) resultSet.getObject(1);
        Object[] structComponents = structObject.getAttributes();
        for (Object component : structComponents){
          System.out.println(component.toString());
        }

The following example queries a standard array of repeated data, then verifies the result:

    // Execute Query
    ResultSet resultSet = statement.executeQuery("SELECT [1,2,3]");
    resultSet.next();
    Object[] arrayObject = (Object[]) resultSet.getArray(1).getArray();
    
    // Verify Result
    int count =0;
    for (; count < arrayObject.length; count++) {
      System.out.println(arrayObject[count]);
    }

The following example queries a `Struct` array of repeated data, then verifies the result:

    // Execute Query
    ResultSet resultSet = statement.executeQuery("SELECT "
        + "[STRUCT(\"Adam\" as name, 12 as age), "
        + "STRUCT(\"Lily\" as name, 17 as age)]");
    
    Struct[] arrayObject = (Struct[]) resultSet.getArray(1).getArray();
    
    // Verify Result
    for (int count =0; count < arrayObject.length; count++) {
      System.out.println(arrayObject[count]);
    }

#### Bulk-insert

The following example performs a bulk-insert operation with the [`executeBatch` method](https://docs.oracle.com/javase/8/docs/api/java/sql/Statement.html#executeBatch--) .

    Connection conn = DriverManager.getConnection(connectionUrl);
    PreparedStatement statement = null;
    Statement st = conn.createStatement();
    final String insertQuery = String.format(
            "INSERT INTO `%s.%s.%s` "
          + " (StringField, IntegerField, BooleanField) VALUES(?, ?, ?);",
            DEFAULT_CATALOG, DATASET, TABLE_NAME);
    
    statement = conn.prepareStatement(insertQuery1);
    
    for (int i=0; i<2000; ++i) {
          statement.setString(1, i+"StringField");
          statement.setInt(2, i);
          statement.setBoolean(3, true);
          statement.addBatch();
    }
    
    statement.executeBatch();

## Logging

To troubleshoot issues with the JDBC driver for BigQuery, you can enable logging by setting connection properties or environment variables. Logging can affect performance and take disk space, so only enable it temporarily to capture an issue.

### Log levels

The `LogLevel` property determines the level of detail that is logged by the `java.util.logging` package:

  - `0` : `OFF` (Default)
  - `1` : `SEVERE`
  - `2` : `WARNING`
  - `3` : `INFO`
  - `4` : `CONFIG`
  - `5` : `FINE`
  - `6` : `FINER`
  - `7` : `FINEST`
  - `8` : `ALL`

We recommend level 6 for general troubleshooting. Levels 7 and 8 are limited to `ResultSet` operations and generate a large volume of logs.

### Enable logging in the connection string

To enable logging in the connection string, add the `LogLevel` and `LogPath` connection properties, for example:

    jdbc:bigquery://https://www.googleapis.com/bigquery/v2:443;ProjectId=MyTestProject;OAuthType=3;LogLevel=6;LogPath=/tmp/jdbc-logs;

### Enable logging with environment variables

If your development tool doesn't allow connection string edits, you can also set the log level and log path with the following environment variables before running your application:

  - `BIGQUERY_JDBC_LOG_LEVEL` : the log level (0-8).
  - `BIGQUERY_JDBC_LOG_PATH` : the directory for log files.

For example, in a Linux or macOS environment, run the following:

    export BIGQUERY_JDBC_LOG_LEVEL=6
    export BIGQUERY_JDBC_LOG_PATH=/tmp/jdbc-logs

## OpenTelemetry

The JDBC driver for BigQuery supports OpenTelemetry (OTel) to provide distributed tracing and logging, which lets you monitor the performance of your database interactions and troubleshoot issues effectively.

### Traced operations

When OpenTelemetry is enabled, the driver generates spans for the following operations:

  - Query execution: Spans are generated for `BigQueryStatement` ( `execute()` , `executeQuery()` , `executeLargeUpdate()` , `executeBatch()` ) and `BigQueryPreparedStatement` ( `execute()` , `executeQuery()` , `executeLargeUpdate()` ).
  - Metadata operations: Spans are generated for specific `DatabaseMetaData` methods ( `getCatalogs()` , `getSchemas()` , `getTables()` , `getColumns()` ).
  - Pagination: Asynchronous fetches for additional pages of results (when using the REST API path) are traced and causally linked to the original query execution span using OpenTelemetry Span Links. A span named `BigQueryStatement.pagination` is created for these operations.
  - Context propagation: The JDBC driver propagates the active context to the underlying `google-cloud-bigquery` SDK. As a result, spans generated by the SDK (such as HTTP RPC calls) automatically appear as children of the JDBC spans, providing a complete end-to-end trace hierarchy.

### Configuration modes

You can configure OpenTelemetry in the JDBC driver using one of the following modes, depending on your application's architecture and requirements.

#### Application-managed telemetry

If your application already uses OpenTelemetry, you can inject your OpenTelemetry instance into the JDBC driver to ensure that the driver's telemetry is correlated with your application's telemetry.

To do this, use the `BigQueryDataSource` API:

    BigQueryDataSource dataSource = new BigQueryDataSource();
    // ... set other properties ...
    dataSource.setCustomOpenTelemetry(yourOpenTelemetryInstance);

#### Global OpenTelemetry support

If you have initialized OpenTelemetry globally in your application (for example, using the OpenTelemetry Java Agent or by calling the `GlobalOpenTelemetry.set()` function), you can configure the driver to use this global instance.

To enable the global instance, set the `UseGlobalOpenTelemetry` connection property to `TRUE` .

#### Zero-configuration Google Cloud telemetry

If you're running on Google Cloud and want a quick setup, you can enable automatic export of traces and logs to Google Cloud observability (Trace and Logging).

To enable this export, set the following connection properties in your JDBC URL:

  - `EnableGcpTraceExporter=true`
  - `EnableGcpLogExporter=true`

The following is an example connection URL:

    jdbc:bigquery://https://www.googleapis.com/bigquery/v2:443;ProjectId=your-project-id;EnableGcpTraceExporter=true;EnableGcpLogExporter=true;

### OpenTelemetry connection properties

The following connection properties are supported for OpenTelemetry. For detailed descriptions and default values, see [Connection properties](https://docs.cloud.google.com/bigquery/docs/jdbc-for-bigquery#connection_properties) .

  - `EnableGcpLogExporter`
  - `EnableGcpTraceExporter`
  - `GcpTelemetryCredentials`
  - `GcpTelemetryProjectId`
  - `UseGlobalOpenTelemetry`

### Important considerations

When deploying OpenTelemetry integration, keep the following considerations in mind regarding logging behavior, authentication, proxy configuration, and pricing.

#### Interaction with LogLevel

The existing `LogLevel` connection property acts as a primary gatekeeper for logging.

  - If `LogLevel=0` (OFF) is set, no log records are generated. Consequently, no logs are exported using OpenTelemetry or to Logging, even if `EnableGcpLogExporter=true` .
  - To enable OTel logging, ensure `LogLevel` is set to a value greater than 0 (for example, `5` for detailed logs).

#### Authentication for telemetry

Telemetry export (both tracing and logging) with the automatic Google Cloud fallback supports both Application Default Credentials (ADC) and explicit Service Account credentials provided using `GcpTelemetryCredentials` .

When `GcpTelemetryProjectId` or `GcpTelemetryCredentials` are provided, both logs and traces are sent to the same specified destination project using the same configured credentials.

#### Proxy configuration with OpenTelemetry and logging

If your application connects to BigQuery through a proxy server, the driver handles proxy routing as follows:

  - **Trace export (HTTP).** When you use the default HTTP protocol for OpenTelemetry trace export ( `otel.exporter.otlp.protocol=http/protobuf` ), the driver automatically routes trace export traffic through the proxy configured in the connection properties using `ProxyHost` and `ProxyPort` .

  - **Log export and gRPC telemetry.** The automatic Google Cloud log exporter ( `EnableGcpLogExporter=true` ) and gRPC-based OpenTelemetry exporters ( `otel.exporter.otlp.protocol=grpc` ) use gRPC, which doesn't support per-connection proxy configuration. To route log export and gRPC telemetry traffic through a proxy server, configure proxy settings at the JVM level using the following system properties:
    
        -Dhttps.proxyHost=PROXY_HOST -Dhttps.proxyPort=PROXY_PORT

#### Required APIs and IAM permissions

To successfully write telemetry data to Google Cloud observability, perform the following setup in your target Google Cloud project:

1.  Enable APIs:
      - Enable the Cloud Trace API ( `cloudtrace.googleapis.com` ).
      - Enable the Cloud Logging API ( `logging.googleapis.com` ).
2.  Grant IAM roles:
      - For exporting traces: Grant the principal or service account the Trace Agent ( `roles/cloudtrace.agent` ) role.
      - For exporting logs: Grant the principal or service account the Logs Writer ( `roles/logging.logWriter` ) role.

#### Pricing and billing

When using zero-configuration Google Cloud telemetry ( `EnableGcpTraceExporter=true` or `EnableGcpLogExporter=true` ), telemetry data is sent to Trace and Logging. These services may incur charges based on the volume of data ingested. For more information, see [Google Cloud Observability](https://cloud.google.com/stackdriver/pricing) .

#### Metrics

This integration doesn't support OpenTelemetry metrics.

#### Dependency shading

To prevent classpath conflicts with your application, the driver shades OpenTelemetry SDK and exporter dependencies. The OpenTelemetry API remains unshaded to allow interoperability with your application-provided SDK.

#### Logging and trace correlation

When OpenTelemetry is enabled, the driver automatically correlates logs with traces:

  - `db.connection_id` : Attached as a span attribute to all JDBC spans.
  - `jdbc.connection_id` : Used as a baggage key and attached as a label to all log entries emitted by the driver to Logging.
  - Trace ID and Span ID: Logs generated within the scope of a query execution automatically include the active `trace_id` and `span_id` .

## Pricing

You can download the JDBC driver for BigQuery at no cost. However, when you use the driver, [standard BigQuery pricing](https://cloud.google.com/bigquery/pricing) applies.

## What's next

  - For additional setup instructions, connection URL property reference manuals, code samples, and local build instructions, visit the open-source repository on GitHub:
      - [User Guide ( `docs/USER_GUIDE.md` )](https://github.com/googleapis/google-cloud-java/blob/main/java-bigquery-jdbc/docs/USER_GUIDE.md)
      - [Development Guide ( `DEVELOPMENT.md` )](https://github.com/googleapis/google-cloud-java/blob/main/java-bigquery-jdbc/DEVELOPMENT.md)
      - [BigQuery Storage APIs Deep Dive ( `docs/STORAGE_APIS.md` )](https://github.com/googleapis/google-cloud-java/blob/main/java-bigquery-jdbc/docs/STORAGE_APIS.md)
  - Learn more about the [ODBC driver for BigQuery](https://docs.cloud.google.com/bigquery/docs/odbc-for-bigquery) .
  - Explore other [BigQuery developer tools](https://docs.cloud.google.com/bigquery/docs/developer-overview) .
