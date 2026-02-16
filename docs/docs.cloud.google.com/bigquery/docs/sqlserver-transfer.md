# Load Microsoft SQL Server data into BigQuery

**Preview**

This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

**Note:** To get support or provide feedback for this feature, contact <dts-preview-support@google.com> .

You can load data from Microsoft SQL Server to BigQuery using the BigQuery Data Transfer Service for Microsoft SQL Server connector. The Microsoft SQL Server connector supports data loads from Microsoft SQL Server instances hosted in on-premises environments and other cloud providers, such as Cloud SQL, Amazon Web Services (AWS), or Microsoft Azure. With the BigQuery Data Transfer Service, you can create on-demand and recurring data transfer jobs to transfer data from your Microsoft SQL Server instance into BigQuery.

## Limitations

Microsoft SQL Server data transfer jobs are subject to the following limitations:

  - There is a limited number of simultaneous connections to a Microsoft SQL Server database. Therefore, the number of simultaneous transfer runs to a single Microsoft SQL Server database is also limited. Ensure that the number of concurrent transfer jobs is less than the maximum number of concurrent connections supported by the Microsoft SQL Server database.
  - Some Microsoft SQL Server data types might be mapped to the `  STRING  ` type in BigQuery to avoid data loss. For example, certain numeric types in Microsoft SQL Server that don't have precision and scale defined might be mapped to `  STRING  ` in BigQuery. For more information, see [Data type mapping](#data_type_mapping) .

## Data ingestion options

The following section provides information about the data ingestion options when you set up a Microsoft SQL Server data transfer.

### TLS configuration

The Microsoft SQL Server connector supports the configuration for transport level security (TLS) to encrypt your data transfers into BigQuery. The Microsoft SQL Server connector supports the following TLS configurations:

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

You can provide PEM-encoded certificates in the **Trusted PEM Certificate** field when you create a Microsoft SQL Server transfer configuration, with the following requirements:

  - The certificate must be a valid PEM-encoded certificate chain.
  - The certificate must be entirely correct. Any missing certificates in the chain or incorrect content causes the TLS connection to fail.
  - For a single certificate, you can provide single, self-signed certificate from the database server.
  - For a full certificate chain issued by a private CA, you must provide the full chain of trust. This includes the certificate from the database server and any intermediate and root CA certificates.

## Before you begin

Before you can schedule a Microsoft SQL Server data transfer, you must meet the following prerequisites.

### Microsoft SQL Server prerequisites

You must have created a user account in the Microsoft SQL Server database. For more information, see [Create a user with a login](https://learn.microsoft.com/en-us/sql/relational-databases/security/authentication-access/create-a-database-user?view=sql-server-ver17#create-a-user-with-a-login) .

### BigQuery prerequisites

  - Verify that you have completed all the actions that are required to [enable the BigQuery Data Transfer Service](/bigquery/docs/enable-transfer-service) .
  - [Create a BigQuery dataset](/bigquery/docs/datasets) to store your data.

#### Required roles

To get the permissions that you need to create a Microsoft SQL Server data transfer, ask your administrator to grant you the [BigQuery Admin](/iam/docs/roles-permissions/bigquery#bigquery.admin) ( `  roles/bigquery.admin  ` ) IAM role on your project. For more information about granting roles, see [Manage access to projects, folders, and organizations](/iam/docs/granting-changing-revoking-access) .

This predefined role contains the permissions required to create a Microsoft SQL Server data transfer. To see the exact permissions that are required, expand the **Required permissions** section:

#### Required permissions

The following permissions are required to create a Microsoft SQL Server data transfer:

  - `  bigquery.transfers.update  `
  - `  bigquery.datasets.get  `

You might also be able to get these permissions with [custom roles](/iam/docs/creating-custom-roles) or other [predefined roles](/iam/docs/roles-overview#predefined) .

### Network configuration

You must set up specific network configurations when a public IP address isn't available for the Microsoft SQL Server database connection. For more information, see the following sections:

  - [Configure a connection to Google Cloud instance](/bigquery/docs/cloud-sql-instance-access)
  - [Configure a connection to AWS](/bigquery/docs/aws-vpn-network-attachment)
  - [Configure a connection to Azure](/bigquery/docs/azure-vpn-network-attachment)

## Set up a Microsoft SQL Server data transfer

Select one of the following options:

### Console

1.  Go to the **Data transfers** page.

2.  Click add **Create transfer** .

3.  In the **Source type** section, for **Source** , select **Microsoft SQL Server** .

4.  In the **Data source details** section, do the following:
    
      - For **Network attachment** , select an existing network attachment or click **Create Network Attachment** .
      - For **Host** , enter the hostname or IP address of the Microsoft SQL Server database.
      - For **Port number** , enter the port number for the Microsoft SQL Server database.
      - For **Database name** , enter the name of the Microsoft SQL Server database.
      - For **Username** , enter the username of the Microsoft SQL Server user initiating the Microsoft SQL Server database connection.
      - For **Password** , enter the password of the Microsoft SQL Server user initiating the Microsoft SQL Server database connection.
      - For **TLS Mode** , select an option from the menu. For more information about TLS modes, see [TLS configuration](#tls_configuration) .
      - For **Trusted PEM Certificate** , enter the public certificate of the certificate authority (CA) that issued the TLS certificate of the database server. For more information, see [Trusted Server Certificate (PEM)](/bigquery/docs/sqlserver-transfer#trusted_server_certificate_pem) .
      - For **Microsoft SQL Server objects to transfer** , browse the Microsoft SQL Server table or manually enter the names of the tables that are required for the transfer.

5.  In the **Destination settings** section, for **Dataset** , select the dataset that you created to store your data, or click **Create new dataset** and create one to use as the destination dataset.

6.  In the **Transfer config name** section, for **Display name** , enter a name for the transfer. The transfer name can be any value that lets you identify the transfer if you need to modify it later.

7.  In the **Schedule options** section, do the following:
    
      - Select a repeat frequency. If you select the **Hours** , **Days** (default), **Weeks** , or **Months** option, you must also specify a frequency. You can also select the **Custom** option to create a more specific repeat frequency. If you select the **On-demand** option, this data transfer only runs when you [manually trigger the transfer](/bigquery/docs/working-with-transfers#manually_trigger_a_transfer) .
      - If applicable, select either the **Start now** or **Start at a set time** option and provide a start date and run time.

8.  Optional: In the **Notification options** section, do the following:
    
      - To enable email notifications, click the **Email notifications** toggle to the on position. When you enable this option, the transfer administrator receives an email notification when a transfer run fails.
      - To configure Pub/Sub run [notifications](/bigquery/docs/transfer-run-notifications) for your transfer, click the **Pub/Sub notifications** toggle to the on position. You can select your [topic](/pubsub/docs/admin) name or click **Create a topic** to create one.

9.  Optional: In the **Advanced options** section, select an encryption type for this transfer. You can select either a Google-owned and Google-managed encryption key or a customer-owned Cloud Key Management Service key. For more information about encryption keys, see [Customer-managed encryption keys (CMEK)](/kms/docs/cmek) .

10. Click **Save** .

### bq

Enter the [`  bq mk  ` command](/bigquery/docs/reference/bq-cli-reference#bq_mk) and supply the transfer creation flag `  --transfer_config  ` :

``` text
bq mk \
    --transfer_config \
    --project_id=PROJECT_ID \
    --data_source=DATA_SOURCE \
    --display_name=DISPLAY_NAME \
    --target_dataset=DATASET \
    --params='PARAMETERS'
```

Replace the following:

  - `  PROJECT_ID  ` (optional): your Google Cloud project ID. If the `  --project_id  ` flag isn't supplied to specify a particular project, the default project is used.

  - `  DATA_SOURCE  ` : the data source, which is `  sqlserver  ` .

  - `  DISPLAY_NAME  ` : the display name for the data transfer configuration. The transfer name can be any value that lets you identify the transfer if you need to modify it later.

  - `  DATASET  ` : the target dataset for the data transfer configuration.

  - `  PARAMETERS  ` : the parameters for the created transfer configuration in JSON format. For example: `  --params='{"param":"param_value"}'  ` . The following are the parameters for a Microsoft SQL Server transfer:
    
      - `  connector.networkAttachment  ` (optional): the name of the network attachment to connect to the Microsoft SQL Server database.
      - `  connector.database  ` : the name of the Microsoft SQL Server database.
      - `  connector.endpoint.host  ` : the hostname or IP address of the database.
      - `  connector.endpoint.port  ` : the port number of the database.
      - `  connector.authentication.username  ` : the username of the database user.
      - `  connector.authentication.password  ` : the password of the database user.
      - `  connector.tls.mode  ` : specify a [TLS configuration](#tls_configuration) to use with this transfer:
          - `  ENCRYPT_VERIFY_CA_AND_HOST  ` to encrypt data, and verify CA and hostname
          - `  ENCRYPT_VERIFY_CA  ` to encrypt data, and verify CA only
          - `  ENCRYPT_VERIFY_NONE  ` for data encryption only
          - `  DISABLE  ` for no encryption or verification
      - `  connector.tls.trustedServerCertificate  ` : (optional) provide one or more [PEM-encoded certificates](/bigquery/docs/sqlserver-transfer#trusted_server_certificate_pem) . Required only if the value of `  connector.tls.mode  ` is `  ENCRYPT_VERIFY_CA_AND_HOST  ` or `  ENCRYPT_VERIFY_CA  ` .
      - `  assets  ` : a list of the names of the Microsoft SQL Server tables to be transferred from the Microsoft SQL Server database as part of the transfer.

For example, the following command creates a Microsoft SQL Server transfer called `  My Transfer  ` :

``` text
bq mk \
    --transfer_config
    --target_dataset=mydataset
    --data_source=sqlserver
    --display_name='My Transfer'
    --params='{"assets":["db1/dbo/Department","db1/dbo/Employees"],
        "connector.authentication.username": "User1",
        "connector.authentication.password":"ABC12345",
        "connector.database":"DB1",
        "connector.endpoint.host":"192.168.0.1",
        "connector.endpoint.port":"1520",
        "connector.networkAttachment":"projects/dev-project1/regions/us-central1/networkattachments/na1",
        "connector.tls.mode": "ENCRYPT_VERIFY_CA_AND_HOST",
        "connector.tls.trustedServerCertificate": "PEM-encoded certificate"}'
```

When you save the transfer configuration, the Microsoft SQL Server connector automatically triggers a transfer run according to your schedule option. With every transfer run, the Microsoft SQL Server connector transfers all available data from Microsoft SQL Server into BigQuery.

To manually run a data transfer outside of your regular schedule, you can start a [backfill run](/bigquery/docs/working-with-transfers#manually_trigger_a_transfer) .

## Data type mapping

The following table maps Microsoft SQL Server data types to the corresponding BigQuery data types:

<table>
<thead>
<tr class="header">
<th>Microsoft SQL Server data type</th>
<th>BigQuery data type</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       tinyint      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       smallint      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       int      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       bigint      </code></td>
<td><code dir="ltr" translate="no">       BIGNUMERIC      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       bit      </code></td>
<td><code dir="ltr" translate="no">       BOOLEAN      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       decimal      </code></td>
<td><code dir="ltr" translate="no">       BIGNUMERIC      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       numeric      </code></td>
<td><code dir="ltr" translate="no">       NUMERIC      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       money      </code></td>
<td><code dir="ltr" translate="no">       BIGNUMERIC      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       smallmoney      </code></td>
<td><code dir="ltr" translate="no">       BIGNUMERIC      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       float      </code></td>
<td><code dir="ltr" translate="no">       FLOAT      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       real      </code></td>
<td><code dir="ltr" translate="no">       FLOAT      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       date      </code></td>
<td><code dir="ltr" translate="no">       DATE      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       time      </code></td>
<td><code dir="ltr" translate="no">       TIME      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       datetime2      </code></td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       datetimeoffset      </code></td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       datetime      </code></td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       smalldatetime      </code></td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       char      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       varchar      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       text      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       nchar      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       nvarchar      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       ntext      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       binary      </code></td>
<td><code dir="ltr" translate="no">       BYTES      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       varbinary      </code></td>
<td><code dir="ltr" translate="no">       BYTES      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       image      </code></td>
<td><code dir="ltr" translate="no">       BYTES      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       geography      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       geometry      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       hierarchyid      </code></td>
<td><code dir="ltr" translate="no">       BYTES      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       rowversion      </code></td>
<td><code dir="ltr" translate="no">       BYTES      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       sql_variant      </code></td>
<td><code dir="ltr" translate="no">       BYTES      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       uniqueidentifier      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       xml      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       json      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       vector      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
</tr>
</tbody>
</table>

The `  json  ` and `  vector  ` data types are only supported in Azure.

The [JSON data type](https://learn.microsoft.com/en-us/sql/t-sql/data-types/json-data-type) is supported in Azure SQL databases and Azure SQL managed instances configured with the always-up-to-date update policy. The JSON data type is not supported in Azure SQL managed instances configured with the Microsoft SQL Server 2022 update policy.

Microsoft SQL Server stores JSON as `  NVARCHAR(MAX)  ` , and not as a JSON type. We recommend that you use `  CHECK (ISJSON(json_col) = 1)  ` for validation, and `  JSON_VALUE()  ` for querying.

The Microsoft SQL Server doesn't have vector support for the `  vector  ` data type. We recommend that you store vectors as JSON arrays in `  NVARCHAR(MAX)  ` and use `  JSON_VALUE()  ` for extraction, with manual `  FLOAT  ` calculations for similarity.

## Troubleshoot

To troubleshoot issues for your data transfer, see [Microsoft SQL Server transfer issues](/bigquery/docs/transfer-troubleshooting#sqlserver-issues) .

## Pricing

There is no cost to transfer Microsoft SQL Server data into BigQuery while this feature is in [Preview](https://cloud.google.com/products#product-launch-stages) .

## What's next

  - For an overview of the BigQuery Data Transfer Service, see [What is BigQuery Data Transfer Service?](/bigquery/docs/dts-introduction) .
  - For information on using transfers, including getting information about a transfer configuration, listing transfer configurations, and viewing a transfer's run history, see [Manage transfers](/bigquery/docs/working-with-transfers) .
