---
name: documents/docs.cloud.google.com/bigquery/docs/connect-to-oracle
uri: https://docs.cloud.google.com/bigquery/docs/connect-to-oracle
title: Connect to Oracle
description: Shows how to connect to Oracle from BigQuery.
data_source: docs.cloud.google.com
---

# Connect to Oracle

> **Preview**
>
> This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

> **Note:** To get support or provide feedback for this preview feature, contact <bq-3p-federation-support@google.com> .

As a BigQuery administrator, you can create a [connection](https://docs.cloud.google.com/bigquery/docs/connections-api-intro) to access Oracle data. This connection enables data analysts to [query data in Oracle](https://docs.cloud.google.com/bigquery/docs/oracle-federated-queries) .

## Supported Oracle environments and versions

BigQuery federation supports the following Oracle deployment environments:

- Oracle Database@Google Cloud
- Oracle Exadata Database Service
- On-premises Oracle instances connected to Google Cloud through Cloud VPN or Cloud Interconnect

BigQuery federation supports the following Oracle versions:

- Oracle Database 23.x (23ai)
- Oracle Database 21.x
- Oracle Database 19.x (19c)

## Before you begin

Enable the necessary APIs, configure your Oracle database, and grant Identity and Access Management roles that give users the necessary permissions to perform each task in this document.

1.  Enable the BigQuery Connection API.

2.  If you plan to route traffic through private networks using network attachments, also enable the Compute Engine API.

3.  In your Oracle database, create a dedicated user credential for BigQuery:

    - [Create a user credential](https://docs.oracle.com/cd/B13789_01/server.101/b10759/statements_8003.htm) in the Oracle database.

    - [Grant `CREATE SESSION` system privileges](https://docs.oracle.com/cd/B13789_01/server.101/b10759/statements_9013.htm) to allow the user to establish a database session:

      ```
      GRANT CREATE SESSION TO USER_NAME;
      ```

    - Grant `SELECT` -only privileges on the tables or views that you intend to query:

      ```
      GRANT SELECT ON SCHEMA_NAME.TABLE_NAME TO USER_NAME;
      ```

    Replace the following:

    - `USER_NAME` : the username for the database user.
    - `SCHEMA_NAME` : the schema of the table that you want to query.
    - `TABLE_NAME` : the table that you want to query.

4.  Configure network connectivity to your Oracle database instance by doing one of the following:

    - If you're routing traffic through private networks, [create a network attachment](https://docs.cloud.google.com/vpc/docs/create-manage-network-attachments) in the same region as your BigQuery connection. DNS peering isn't supported; connect using an IP address or a hostname resolvable within your VPC network.
    - If you're connecting over the public internet, add all [Google IP address ranges](https://www.gstatic.com/ipranges/goog.json) to the firewall rules of your Oracle database.

### Required roles

To get the permissions that you need to connect to Oracle, ask your administrator to grant you the following IAM roles:

- To create a connection: [BigQuery Connection Admin](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.connectionAdmin) ( `roles/bigquery.connectionAdmin` ) on the project
- To configure network attachments: [Compute Admin](https://docs.cloud.google.com/iam/docs/roles-permissions/compute#compute.admin) ( `roles/compute.admin` ) on the project

For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

You might also be able to get the required permissions through [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

## Connect BigQuery to Oracle

You can connect BigQuery to Oracle in the Google Cloud console or the bq command-line tool.

### Console

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the **Explorer** pane, click add **Add data** .

    The **Add data** page opens.

3.  In the **Filter By** pane, in the **Data Source Type** section, select **Databases** .

    Alternatively, in the **Search for data sources** field, enter `oracle` .

4.  In the **Featured data sources** section, click **Oracle** .

5.  In the **Access external data in place** section, click the **BigQuery Federation** solution card with the description **Federated queries to Oracle** .

    The **External data source** pane opens.

6.  In the **External data source** pane, configure the following:

    - In the **Connection ID** field, enter a unique connection ID (for example, `oracle_prod_conn` ).
    - In the **Location type** section, select **Region** , and then select the region where your BigQuery dataset resides. Queries that use this connection must be run from this region.
    - (Optional) In the **Friendly name** field, enter a descriptive name for the connection.
    - (Optional) In the **Description** field, enter a description for this connection resource.
    - In the **Encryption** section, select **Google-managed encryption key** , or select **Cloud KMS key** to use a [customer-managed encryption key (CMEK)](https://docs.cloud.google.com/bigquery/docs/customer-managed-encryption) .
    - In the **Host:port** field, enter the host and port of the Oracle database server in `HOST:PORT` format (for example, `10.10.1.2:1521` or `db.example.com:2484` ).
    - In the **Username** field, enter the database user that you created in the prerequisites.
    - In the **Password** field, enter the database user's password.
    - In the **Database** field, enter the Oracle database Service Name.
    - (Optional) In the **Network attachment** field, if you're using private connectivity, enter the resource path of the network attachment in the `projects/ `` PROJECT_ID `` /regions/ `` NA_REGION `` /networkAttachments/ `` ATTACHMENT_NAME` format.
    - In the **TLS mode** list, select one of the supported [TLS modes](https://docs.cloud.google.com/bigquery/docs/connect-to-oracle#tls-configuration) (for example, **Encrypt data, verify CA and host name (recommended)** ).
    - In the **Certificate authority (CA)** list, select **Public CA (Web PKI)** , or select a custom CA and paste the PEM-formatted certificate.

7.  Click **Create connection** .

### bq

Use the [`bq mk` command](https://docs.cloud.google.com/bigquery/docs/reference/bq-cli-reference#bq_mk) with the `--connection` flag:

```
bq mk --connection \
  --location=LOCATION \
  --project_id=PROJECT_ID \
  --connector_configuration '{
    "connector_id": "oracle",
    "endpoint": {
      "host_port": "HOST_PORT"
    },
    "asset": {
      "database": "DATABASE"
    },
    "authentication": {
      "username_password": {
        "username": "USERNAME",
        "password": {
          "plaintext": "PASSWORD"
        }
      }
    },
    "tls": {
      "mode": "TLS_MODE"
    },
    "network": {
      "private_service_connect": {
        "network_attachment": "projects/PROJECT_ID/regions/NA_REGION/networkAttachments/ATTACHMENT_NAME"
      }
    }
  }' \
  CONNECTION_ID
```

Replace the following:

- `LOCATION` : the BigQuery region (for example, `us-central1` ) matching the dataset that you intend to query together with Oracle. Queries that use this connection must be run from this region.
- `PROJECT_ID` : your Google Cloud project ID.
- `HOST_PORT` : the host and port of your Oracle database server in the `HOST:PORT` format (for example, `10.10.1.2:1521` ).
- `DATABASE` : the Oracle database Service Name.
- `USERNAME` : the Oracle database user.
- `PASSWORD` : the database user's password.
- `TLS_MODE` : the [TLS encryption mode](https://docs.cloud.google.com/bigquery/docs/connect-to-oracle#tls-configuration) ( `ENCRYPT_VERIFY_CA_AND_HOST` , `ENCRYPT_VERIFY_CA` , `ENCRYPT_VERIFY_NONE` , or `DISABLE` ). If you use a custom CA certificate with `ENCRYPT_VERIFY_CA_AND_HOST` or `ENCRYPT_VERIFY_CA` , include the `"private_pki": { "trusted_certificates_pem": " `` CERT_CONTENT `` " }` object under `"tls"` .
- `NA_REGION` : the region where your network attachment is located.
- `ATTACHMENT_NAME` : the name of your network attachment. If connecting over public IP, omit the `"network"` object.
- `CONNECTION_ID` : the unique identifier for this connection.
- (Optional) `--kms_key_name= `` KMS_KEY_NAME` : a customer-managed encryption key (CMEK). If omitted, credentials are protected by the default Google-owned and Google-managed encryption key.

## Transport Layer Security (TLS) configuration

The Oracle connector supports Transport Layer Security (TLS) to encrypt query traffic in transit between BigQuery and your Oracle database.

When you connect BigQuery to Oracle, select one of the following TLS modes:

- **Encrypt data, and verify Certificate Authority (CA) and hostname** ( `ENCRYPT_VERIFY_CA_AND_HOST` mode). Performs full server validation using TLS. Encrypts all data in transit, verifies that the database server's certificate is signed by a trusted CA, and checks that the hostname that you're connecting to matches the Common Name (CN) or Subject Alternative Name (SAN) in the certificate. Mandatory for connections over public IPs.

- **Encrypt data, and verify CA only** ( `ENCRYPT_VERIFY_CA` mode). Encrypts all data in transit and verifies that the server's certificate is signed by a trusted CA, but doesn't verify the server's hostname. Use this mode if the server certificate is signed by a trusted CA, but you connect using an IP address or a hostname that doesn't match the certificate CN or SAN.

- **Encryption only** ( `ENCRYPT_VERIFY_NONE` mode). Encrypts all data transferred between BigQuery and the server using Oracle network encryption over the standard TCP port. Doesn't perform certificate or hostname verification. Recommended only within private VPCs.

- **No encryption or verification** ( `DISABLE` mode). Doesn't encrypt data and doesn't perform certificate or hostname verification. Permitted only when connecting through private network attachments within protected VPC networks.

#### Trusted server certificates in PEM format

If you use either the `ENCRYPT_VERIFY_CA_AND_HOST` mode or the `ENCRYPT_VERIFY_CA` mode, do the following:

- If your database server certificate is signed by a public CA (such as those included in the Mozilla Root CA Program, including Let's Encrypt, DigiCert, or Google Trust Services), you don't need to provide a certificate. Root certificates for public CAs are trusted by default.
- If you use a certificate signed by an internal or private CA within your organization, or a self-signed certificate, you must provide the full certificate chain in Privacy-Enhanced Mail (PEM) format in the **Trusted PEM certificate** field during connection setup.

## Share connections with users

You can grant the following roles to let users query data and manage connections:

- `roles/bigquery.connectionUser` : enables users to use connections to connect with external data sources and run queries on them.

- `roles/bigquery.connectionAdmin` : enables users to manage connections.

For more information about IAM roles and permissions in BigQuery, see [Predefined roles and permissions](https://docs.cloud.google.com/bigquery/access-control) .

Select one of the following options:

### Console

1.  Go to the **BigQuery** page.

    Connections are listed in your project, in a group called **Connections** .

2.  In the left pane, click explore **Explorer** :

    ![Highlighted button for the Explorer pane.](https://docs.cloud.google.com/static/bigquery/images/explorer-tab.png)

    If you don't see the left pane, click last_page **Expand left pane** to open the pane.

3.  Click your project, click **Connections** , and then select a connection.

4.  In the **Details** pane, click **Share** to share a connection. Then do the following:

    1.  In the **Connection permissions** dialog, share the connection with other principals by adding or editing principals.

    2.  Click **Save** .

### bq

You cannot share a connection with the bq command-line tool. To share a connection, use the Google Cloud console or the BigQuery Connections API method to share a connection.

### API

Use the [`projects.locations.connections.setIAM` method](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rest/v1/projects.locations.connections#methods) in the BigQuery Connections REST API reference section, and supply an instance of the `policy` resource.

### Java

Before trying this sample, follow the Java setup instructions in the [BigQuery quickstart using client libraries](https://docs.cloud.google.com/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Java API reference documentation](https://docs.cloud.google.com/java/docs/reference/google-cloud-bigquery/latest/overview) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](https://docs.cloud.google.com/bigquery/docs/authentication#client-libs) .

```java
import com.google.api.resourcenames.ResourceName;
import com.google.cloud.bigquery.connection.v1.ConnectionName;
import com.google.cloud.bigqueryconnection.v1.ConnectionServiceClient;
import com.google.iam.v1.Binding;
import com.google.iam.v1.Policy;
import com.google.iam.v1.SetIamPolicyRequest;
import java.io.IOException;

// Sample to share connections
public class ShareConnection {

  public static void main(String[] args) throws IOException {
    // TODO(developer): Replace these variables before running the sample.
    String projectId = "MY_PROJECT_ID";
    String location = "MY_LOCATION";
    String connectionId = "MY_CONNECTION_ID";
    shareConnection(projectId, location, connectionId);
  }

  static void shareConnection(String projectId, String location, String connectionId)
      throws IOException {
    try (ConnectionServiceClient client = ConnectionServiceClient.create()) {
      ResourceName resource = ConnectionName.of(projectId, location, connectionId);
      Binding binding =
          Binding.newBuilder()
              .addMembers("group:example-analyst-group@google.com")
              .setRole("roles/bigquery.connectionUser")
              .build();
      Policy policy = Policy.newBuilder().addBindings(binding).build();
      SetIamPolicyRequest request =
          SetIamPolicyRequest.newBuilder()
              .setResource(resource.toString())
              .setPolicy(policy)
              .build();
      client.setIamPolicy(request);
      System.out.println("Connection shared successfully");
    }
  }
}
```

## Pricing

Federated queries and connections are subject to the following charges:

- Standard [federated query pricing](https://docs.cloud.google.com/bigquery/docs/federated-queries-intro#pricing) applies.
- Using VPC is subject to [Virtual Private Cloud pricing](https://docs.cloud.google.com/vpc/pricing) .
- Using Cloud VPN is subject to [Cloud VPN pricing](https://docs.cloud.google.com/network-connectivity/docs/vpn/pricing) .
- Using Cloud NAT is subject to [Cloud NAT pricing](https://docs.cloud.google.com/nat/pricing) .

## What's next

- Learn about different [connection types](https://docs.cloud.google.com/bigquery/docs/connections-api-intro) .
- Learn about [managing connections](https://docs.cloud.google.com/bigquery/docs/working-with-connections) .
- Learn how to [query Oracle data](https://docs.cloud.google.com/bigquery/docs/oracle-federated-queries) .
