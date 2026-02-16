# Load MySQL data into BigQuery

You can load data from MySQL to BigQuery using the BigQuery Data Transfer Service for MySQL connector. It supports MySQL instances that are hosted in your on-premises environment, in [Cloud SQL](/sql/docs/introduction) , and in other public cloud providers such as Amazon Web Services (AWS) and Microsoft Azure. With the BigQuery Data Transfer Service, you can schedule recurring transfer jobs that add your latest data from MySQL to BigQuery.

## Before you begin

  - [Create a user](https://dev.mysql.com/doc/mysql-monitor/8.0/en/mem-acl-creating-user-roles-tasks.html) in the MySQL database.
  - Verify that you have completed all the actions that are required to [enable the BigQuery Data Transfer Service](/bigquery/docs/enable-transfer-service) .
  - [Create a BigQuery dataset](/bigquery/docs/datasets) to store your data.
  - Verify that you have the [required roles](#required-roles) to complete the tasks in this document.

### Required roles

To get the permissions that you need to create a BigQuery Data Transfer Service data transfer, ask your administrator to grant you the [BigQuery Admin](/iam/docs/roles-permissions/bigquery#bigquery.admin) ( `  roles/bigquery.admin  ` ) IAM role on your project. For more information about granting roles, see [Manage access to projects, folders, and organizations](/iam/docs/granting-changing-revoking-access) .

This predefined role contains the permissions required to create a BigQuery Data Transfer Service data transfer. To see the exact permissions that are required, expand the **Required permissions** section:

#### Required permissions

The following permissions are required to create a BigQuery Data Transfer Service data transfer:

  - BigQuery Data Transfer Service permissions:
      - `  bigquery.transfers.update  `
      - `  bigquery.transfers.get  `
  - BigQuery permissions:
      - `  bigquery.datasets.get  `
      - `  bigquery.datasets.getIamPolicy  `
      - `  bigquery.datasets.update  `
      - `  bigquery.datasets.setIamPolicy  `
      - `  bigquery.jobs.create  `

You might also be able to get these permissions with [custom roles](/iam/docs/creating-custom-roles) or other [predefined roles](/iam/docs/roles-overview#predefined) .

For more information, see [Grant `  bigquery.admin  ` access](/bigquery/docs/enable-transfer-service#grant_bigqueryadmin_access) .

If you intend to set up transfer run notifications for Pub/Sub, ensure that you have the `  pubsub.topics.setIamPolicy  ` Identity and Access Management (IAM) permission. Pub/Sub permissions are not required if you only set up email notifications. For more information, see [BigQuery Data Transfer Service run notifications](/bigquery/docs/transfer-run-notifications) .

### Network connections

If a public IP address is not available for the MySQL database connection, you must [set up a network attachment](/vpc/docs/create-manage-network-attachments) .

For detailed instructions on the required network setup, refer to the following documents:

  - If you're transferring from Cloud SQL, see [Configure Cloud SQL instance access](/bigquery/docs/cloud-sql-instance-access) .
  - If you're transferring from AWS, see [Set up the AWS-Google Cloud VPN and network attachment](/bigquery/docs/aws-vpn-network-attachment) .
  - If you're transferring from Azure, see [Set up the Azure-Google Cloud VPN and network attachment](/bigquery/docs/azure-vpn-network-attachment) .

## Limitations

MySQL data transfers are subject to following limitations:

  - The maximum number of simultaneous connections to a MySQL database is determined by the MySQL configuration parameter `  max_connections  ` . By default, this is set to 151 connections, but it can be configured to a higher limit as needed. As a result, the number of simultaneous transfer runs to a single MySQL database is limited to that maximum amount. This limitation also means that the number of concurrent transfer jobs should be limited to a value less than the maximum number of concurrent connections supported by the MySQL database.
  - A single transfer configuration can only support one data transfer run at a given time. In the case where a second data transfer is scheduled to run before the first transfer is completed, then only the first data transfer completes while any other data transfers that overlap with the first transfer is skipped.
      - To avoid skipped transfers within a single transfer configuration, we recommend that you increase the duration of time between large data transfers by configuring the **Repeat frequency** .
  - During a data transfer, the MySQL connector identifies indexed and partitioned key columns to transfer your data in parallel batches. For this reason, we recommend that you specify primary key columns or use indexed columns in your table to improve the performance and reduce the error rate in your data transfers.
      - If you have indexed or primary key constraints, only the following column types are supported for creating parallel batches:
          - `  INTEGER  `
          - `  TINYINT  `
          - `  SMALLINT  `
          - `  FLOAT  `
          - `  REAL  `
          - `  DOUBLE  `
          - `  NUMERIC  `
          - `  BIGINT  `
          - `  DECIMAL  `
          - `  DATE  `
      - MySQL data transfers that don't use primary key or indexed columns can't support more than 2,000,000 records per table.

## Data ingestion options

The following sections provide information about the data ingestion options when you set up a MySQL data transfer.

### TLS configuration

The MySQL connector supports the configuration for transport level security (TLS) to encrypt your data transfers into BigQuery. The MySQL connector supports the following TLS configurations:

  - **Encrypt data, and verify CA and hostname** : This mode performs a full validation of the server using TLS over the TCPS protocol. It encrypts all data in transit and verifies that the database server's certificate is signed by a trusted Certificate Authority (CA). This mode also checks that the hostname you're connecting to exactly matches the Common Name (CN) or a Subject Alternative Name (SAN) on the server's certificate. This mode prevents attackers from using a valid certificate for a different domain to impersonate your database server.
      - If your hostname does not match the certificate CN or SAN, the connection fails. You must configure a DNS resolution to match the certificate or use a different security mode.
      - Use this mode for the most secure option to prevent person-in-the-middle (PITM) attacks.
  - **Encrypt data, and verify CA only** : This mode encrypts all data using TLS over the TCPS protocol and verifies that the server's certificate is signed by a CA that the client trusts. However, this mode does not verify the server's hostname. This mode successfully connects as long as the certificate is valid and issued by a trusted VA, regardless of whether the hostname in the certificate matches the hostname you are connecting to.
      - Use this mode if you want to ensure that you are connecting to a server whose certificate is signed by a trusted CA, but the hostname is not verifiable or you don't have control over the hostname configuration.
  - **Encryption only** : This mode encrypts all data transferred between the client and the server. It does not perform any certificate or hostname validation.
      - This mode provides some level of security by protecting data in transit, but it can be vulnerable to PITM attacks.
      - Use this mode if you need to ensure all data is encrypted but can't or don't want to verify the server's identity. We recommend using this mode when working with private VPCs.
  - **No encryption or verification** : This mode does not encrypt any data and does not perform any certificate or hostname verification. All data is sent as plain text.
      - We don't recommend using this mode in an environment where sensitive data is handled.
      - We only recommend using this mode for testing purposes on an isolated network where security is not a concern.

#### Trusted Server Certificate (PEM)

If you are using either the **Encrypt data, and verify CA and hostname** mode or the **Encrypt data, and verify CA** mode, then you can also provide one or more PEM-encoded certificates. These certificates are required in some scenarios where the BigQuery Data Transfer Service needs to verify the identity of your database server during the TLS connection:

  - If you are using a certificate signed by a private CA within your organization or a self-signed certificate, you must provide the full certificate chain or the single self-signed certificate. This is required for certificates issued by internal CAs of managed cloud provider services, such as the Amazon Relational Database Service (RDS).
  - If your database server certificate is signed by a public CA (for example, Let's Encrypt, DigiCert, or GlobalSign), you don't need to provide a certificate. The root certificates for these public CAs are pre-installed and trusted by the BigQuery Data Transfer Service.

You can provide PEM-encoded certificates in the **Trusted PEM Certificate** field when you create a MySQL transfer configuration, with the following requirements:

  - The certificate must be a valid PEM-encoded certificate chain.
  - The certificate must be entirely correct. Any missing certificates in the chain or incorrect content causes the TLS connection to fail.
  - For a single certificate, you can provide single, self-signed certificate from the database server.
  - For a full certificate chain issued by a private CA, you must provide the full chain of trust. This includes the certificate from the database server and any intermediate and root CA certificates.

## Load MySQL data into BigQuery

Add MySQL data into BigQuery by setting up a transfer configuration using one of the following options:

### Console

1.  Go to the **Data transfers** page.

2.  Click add **Create transfer** .

3.  In the **Source type** section, for **Source** , select **MySQL** .

4.  In the **Transfer config name** section, for **Display name** , enter a name for the transfer. The transfer name can be any value that lets you identify the transfer if you need to modify it later.

5.  In the **Schedule options** section, do the following:
    
      - Select a repeat frequency. If you select the **Hours** , **Days** (default), **Weeks** , or **Months** option, you must also specify a frequency. You can also select the **Custom** option to create a more specific repeat frequency. If you select the **On-demand** option, this data transfer only runs when you [manually trigger the transfer](/bigquery/docs/working-with-transfers#manually_trigger_a_transfer) .
      - If applicable, select either the **Start now** or **Start at a set time** option and provide a start date and run time.

6.  In the **Destination settings** section, for **Dataset** , select the dataset that you created to store your data, or click **Create new dataset** and create one to use as the destination dataset.

7.  In the **Data source details** section, do the following:
    
      - For **Network attachment** , select an existing network attachment or click **Create Network Attachment** . For more information, see the [Network connections](#network-connections) section of this document.
    
      - For **Host** , enter the hostname or IP address of the MySQL database server.
    
      - For **Port number** , enter the port number for the MySQL database server.
    
      - For **Database name** , enter the name of the MySQL database.
    
      - For **Username** , enter the username of the MySQL user initiating the MySQL database connection.
    
      - For **Password** , enter the password of the MySQL user initiating the MySQL database connection.
    
      - For **TLS Mode** , select an option from the menu. For more information about TLS modes, see [TLS configuration](#tls_configuration) .
    
      - For **Trusted PEM Certificate** , enter the public certificate of the certificate authority (CA) that issued the TLS certificate of the database server. For more information, see [Trusted Server Certificate (PEM)](/bigquery/docs/mysql-transfer#trusted_server_certificate_pem) .
    
      - For **MySQL objects to transfer** , do one of the following:
        
          - Click **Browse** to select the MySQL tables that are required for the transfer, and then click **Select** .
          - Manually enter the names of the tables in the MySQL objects to transfer.

8.  Optional: In the **Notification options** section, do the following:
    
      - To enable email notifications, click the **Email notifications** toggle to the on position. When you enable this option, the transfer administrator receives an email notification when a transfer run fails.
      - To configure Pub/Sub run [notifications](/bigquery/docs/transfer-run-notifications) for your transfer, click the **Pub/Sub notifications** toggle to the on position. You can select your [topic](/pubsub/docs/admin) name or click **Create a topic** to create one.

9.  Click **Save** .

### bq

Enter the [`  bq mk  ` command](/bigquery/docs/reference/bq-cli-reference#bq_mk) and supply the transfer creation flag `  --transfer_config  ` :

``` text
bq mk
    --transfer_config
    --project_id=PROJECT_ID
    --data_source=DATA_SOURCE
    --display_name=DISPLAY_NAME
    --target_dataset=DATASET
    --params='PARAMETERS'
```

Replace the following:

  - PROJECT\_ID (optional): your Google Cloud project ID. If the `  --project_id  ` flag isn't supplied to specify a particular project, the default project is used.

  - DATA\_SOURCE : the data source, which is `  mysql  ` .

  - DISPLAY\_NAME : the display name for the data transfer configuration. The transfer name can be any value that lets you identify the transfer if you need to modify it later.

  - DATASET : the target dataset for the data transfer configuration.

  - PARAMETERS : the parameters for the created transfer configuration in JSON format. For example: `  --params='{"param":"param_value"}'  ` . The following are the parameters for a MySQL transfer:
    
      - `  connector.networkAttachment  ` (optional): the name of the network attachment to connect to the MySQL database.
      - `  connector.database  ` : the name of the MySQL database.
      - `  connector.endpoint.host  ` : the hostname or IP address of the database.
      - `  connector.endpoint.port  ` : the port number of the database.
      - `  connector.authentication.username  ` : the username of the database user.
      - `  connector.authentication.password  ` : the password of the database user. connector.connectionType
      - `  connector.connectionType  ` (optional): the connection type to determine the connection URL. This can be `  SERVICE  ` , `  SID  ` , or `  TNS  ` . When not provided, this defaults to `  SERVICE  ` .
      - `  connector.tls.mode  ` : specify a [TLS configuration](#tls_configuration) to use with this transfer:
          - `  ENCRYPT_VERIFY_CA_AND_HOST  ` to encrypt data, and verify CA and hostname
          - `  ENCRYPT_VERIFY_CA  ` to encrypt data, and verify CA only
          - `  ENCRYPT_VERIFY_NONE  ` for data encryption only
          - `  DISABLE  ` for no encryption or verification
      - `  connector.tls.trustedServerCertificate  ` : (optional) provide one or more [PEM-encoded certificates](/bigquery/docs/mysql-transfer#trusted_server_certificate_pem) . Required only if `  connector.tls.mode  ` is `  ENCRYPT_VERIFY_CA_AND_HOST  ` or `  ENCRYPT_VERIFY_CA  ` .
      - `  assets  ` : a list of the names of the MySQL tables to be transferred from the MySQL database as part of the transfer.

For example, the following command creates a MySQL transfer called `  My Transfer  ` :

``` text
bq mk
    --transfer_config
    --target_dataset=mydataset
    --data_source=mysql
    --display_name='My Transfer'
    --params='{"assets":["DB1/DEPARTMENT","DB1/EMPLOYEES"],
        "connector.authentication.username": "User1",
        "connector.authentication.password":"ABC12345",
        "connector.encryptionMode":"FULL",
        "connector.database":"DB1",
        "connector.endpoint.host":"54.74.220.23",
        "connector.endpoint.port":3306
        "connector.tls.mode": "ENCRYPT_VERIFY_CA_AND_HOST",
        "connector.tls.trustedServerCertificate": "PEM-encoded certificate"}'
```

### API

Use the [`  projects.locations.transferConfigs.create  ` method](/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs/create) and supply an instance of the [`  TransferConfig  ` resource](/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs#TransferConfig) .

When you save the transfer configuration, the MySQL connector automatically triggers a transfer run according to your schedule option. With every transfer run, the MySQL connector transfers all available data from MySQL into BigQuery.

To manually run a data transfer outside of your regular schedule, you can start a [backfill run](/bigquery/docs/working-with-transfers#manually_trigger_a_transfer) .

## Data type mapping

The following table maps MySQL data types to the corresponding BigQuery data types.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>MySQL data type</th>
<th>BigQuery data type</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       BIT      </code></td>
<td><code dir="ltr" translate="no">       BOOLEAN      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       TINYINT      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       BOOL      </code> , <code dir="ltr" translate="no">       BOOLEAN      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code>
<p>In a MySQL database, the <code dir="ltr" translate="no">        BOOL       </code> and <code dir="ltr" translate="no">        BOOLEAN       </code> data types are internally stored as <code dir="ltr" translate="no">        TINYINT(1)       </code> , which supports values in the range <code dir="ltr" translate="no">        -128       </code> to <code dir="ltr" translate="no">        127       </code> . For this reason, <code dir="ltr" translate="no">        BOOL       </code> and <code dir="ltr" translate="no">        BOOLEAN       </code> data types are mapped to <code dir="ltr" translate="no">        INTEGER       </code> when transferred to BigQuery. For more information, see <a href="https://dev.mysql.com/doc/refman/8.4/en/numeric-type-syntax.html">Numeric Data Type Syntax</a> .</p></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       SMALLINT      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       MEDIUMINT      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       INT      </code> , <code dir="ltr" translate="no">       INTEGER      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       BIGINT      </code></td>
<td><code dir="ltr" translate="no">       BIGNUMERIC      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       FLOAT      </code></td>
<td><code dir="ltr" translate="no">       FLOAT      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       DOUBLE      </code></td>
<td><code dir="ltr" translate="no">       FLOAT      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       DECIMAL      </code></td>
<td><code dir="ltr" translate="no">       BIGNUMERIC      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       DATE      </code></td>
<td><code dir="ltr" translate="no">       DATE      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       DATETIME      </code></td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       TIME      </code></td>
<td><code dir="ltr" translate="no">       TIME      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       YEAR      </code></td>
<td><code dir="ltr" translate="no">       DATE      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       CHAR      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       VARCHAR      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       BINARY      </code></td>
<td><code dir="ltr" translate="no">       BYTES      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       VARBINARY      </code></td>
<td><code dir="ltr" translate="no">       BYTES      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       TINYBLOB      </code></td>
<td><code dir="ltr" translate="no">       BYTES      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       TINYTEXT      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       BLOB      </code></td>
<td><code dir="ltr" translate="no">       BYTES      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       TEXT      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       MEDIUMBLOB      </code></td>
<td><code dir="ltr" translate="no">       BYTES      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       MEDIUMTEXT      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       LONGBLOB      </code></td>
<td><code dir="ltr" translate="no">       BYTES      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       LONGTEXT      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       ENUM      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       SET      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       JSON      </code></td>
<td><code dir="ltr" translate="no">       JSON      </code></td>
</tr>
</tbody>
</table>

## Troubleshoot

If you are having issues setting up your data transfer, see [MySQL transfer issues](/bigquery/docs/transfer-troubleshooting#mysql-issues) .

## Pricing

For pricing information about MySQL transfers, see [Data Transfer Service pricing](/bigquery/pricing#data-transfer-service-pricing) .

## What's next

  - For an overview of the BigQuery Data Transfer Service, see [What is BigQuery Data Transfer Service?](/bigquery/docs/dts-introduction) .
  - For information on using transfers, including getting information about a transfer configuration, listing transfer configurations, and viewing a transfer's run history, see [Manage transfers](/bigquery/docs/working-with-transfers) .
  - Learn how to [load data with cross-cloud operations](/bigquery/docs/load-data-using-cross-cloud-transfer) .
