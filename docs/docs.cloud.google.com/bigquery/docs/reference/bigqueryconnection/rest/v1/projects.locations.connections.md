  - [Resource: Connection](#Connection)
      - [JSON representation](#Connection.SCHEMA_REPRESENTATION)
  - [CloudSqlProperties](#CloudSqlProperties)
      - [JSON representation](#CloudSqlProperties.SCHEMA_REPRESENTATION)
  - [DatabaseType](#DatabaseType)
  - [CloudSqlCredential](#CloudSqlCredential)
      - [JSON representation](#CloudSqlCredential.SCHEMA_REPRESENTATION)
  - [AwsProperties](#AwsProperties)
      - [JSON representation](#AwsProperties.SCHEMA_REPRESENTATION)
  - [AwsAccessRole](#AwsAccessRole)
      - [JSON representation](#AwsAccessRole.SCHEMA_REPRESENTATION)
  - [AzureProperties](#AzureProperties)
      - [JSON representation](#AzureProperties.SCHEMA_REPRESENTATION)
  - [CloudSpannerProperties](#CloudSpannerProperties)
      - [JSON representation](#CloudSpannerProperties.SCHEMA_REPRESENTATION)
  - [CloudResourceProperties](#CloudResourceProperties)
      - [JSON representation](#CloudResourceProperties.SCHEMA_REPRESENTATION)
  - [SparkProperties](#SparkProperties)
      - [JSON representation](#SparkProperties.SCHEMA_REPRESENTATION)
  - [MetastoreServiceConfig](#MetastoreServiceConfig)
      - [JSON representation](#MetastoreServiceConfig.SCHEMA_REPRESENTATION)
  - [SparkHistoryServerConfig](#SparkHistoryServerConfig)
      - [JSON representation](#SparkHistoryServerConfig.SCHEMA_REPRESENTATION)
  - [SalesforceDataCloudProperties](#SalesforceDataCloudProperties)
      - [JSON representation](#SalesforceDataCloudProperties.SCHEMA_REPRESENTATION)
  - [ConnectorConfiguration](#ConnectorConfiguration)
      - [JSON representation](#ConnectorConfiguration.SCHEMA_REPRESENTATION)
  - [Endpoint](#Endpoint)
      - [JSON representation](#Endpoint.SCHEMA_REPRESENTATION)
  - [Authentication](#Authentication)
      - [JSON representation](#Authentication.SCHEMA_REPRESENTATION)
  - [UsernamePassword](#UsernamePassword)
      - [JSON representation](#UsernamePassword.SCHEMA_REPRESENTATION)
  - [Secret](#Secret)
      - [JSON representation](#Secret.SCHEMA_REPRESENTATION)
  - [SecretType](#SecretType)
  - [Network](#Network)
      - [JSON representation](#Network.SCHEMA_REPRESENTATION)
  - [PrivateServiceConnect](#PrivateServiceConnect)
      - [JSON representation](#PrivateServiceConnect.SCHEMA_REPRESENTATION)
  - [Asset](#Asset)
      - [JSON representation](#Asset.SCHEMA_REPRESENTATION)
  - [Methods](#METHODS_SUMMARY)

## Resource: Connection

Configuration parameters to establish connection with an external data source, except the credential attributes.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;name&quot;: string,
  &quot;friendlyName&quot;: string,
  &quot;description&quot;: string,
  &quot;configuration&quot;: {
    object (ConnectorConfiguration)
  },
  &quot;creationTime&quot;: string,
  &quot;lastModifiedTime&quot;: string,
  &quot;hasCredential&quot;: boolean,
  &quot;kmsKeyName&quot;: string,

  // Union field properties can be only one of the following:
  &quot;cloudSql&quot;: {
    object (CloudSqlProperties)
  },
  &quot;aws&quot;: {
    object (AwsProperties)
  },
  &quot;azure&quot;: {
    object (AzureProperties)
  },
  &quot;cloudSpanner&quot;: {
    object (CloudSpannerProperties)
  },
  &quot;cloudResource&quot;: {
    object (CloudResourceProperties)
  },
  &quot;spark&quot;: {
    object (SparkProperties)
  },
  &quot;salesforceDataCloud&quot;: {
    object (SalesforceDataCloudProperties)
  }
  // End of list of possible types for union field properties.
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  name  `

`  string  `

Output only. The resource name of the connection in the form of: `  projects/{projectId}/locations/{locationId}/connections/{connectionId}  `

`  friendlyName  `

`  string  `

User provided display name for the connection.

`  description  `

`  string  `

User provided description.

`  configuration  `

`  object ( ConnectorConfiguration  ` )

Optional. Connector configuration.

`  creationTime  `

`  string ( int64 format)  `

Output only. The creation timestamp of the connection.

`  lastModifiedTime  `

`  string ( int64 format)  `

Output only. The last update timestamp of the connection.

`  hasCredential  `

`  boolean  `

Output only. True, if credential is configured for this connection.

`  kmsKeyName  `

`  string  `

Optional. The Cloud KMS key that is used for credentials encryption.

If omitted, internal Google owned encryption keys are used.

Example: `  projects/[kms_project_id]/locations/[region]/keyRings/[key_region]/cryptoKeys/[key]  `

Union field `  properties  ` . Properties specific to the underlying data source. `  properties  ` can be only one of the following:

`  cloudSql  `

`  object ( CloudSqlProperties  ` )

Cloud SQL properties.

`  aws  `

`  object ( AwsProperties  ` )

Amazon Web Services (AWS) properties.

`  azure  `

`  object ( AzureProperties  ` )

Azure properties.

`  cloudSpanner  `

`  object ( CloudSpannerProperties  ` )

Cloud Spanner properties.

`  cloudResource  `

`  object ( CloudResourceProperties  ` )

Cloud Resource properties.

`  spark  `

`  object ( SparkProperties  ` )

Spark properties.

`  salesforceDataCloud  `

`  object ( SalesforceDataCloudProperties  ` )

Optional. Salesforce DataCloud properties. This field is intended for use only by Salesforce partner projects. This field contains properties for your Salesforce DataCloud connection.

## CloudSqlProperties

Connection properties specific to the Cloud SQL.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;instanceId&quot;: string,
  &quot;database&quot;: string,
  &quot;type&quot;: enum (DatabaseType),
  &quot;credential&quot;: {
    object (CloudSqlCredential)
  },
  &quot;serviceAccountId&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  instanceId  `

`  string  `

Cloud SQL instance ID in the form `  project:location:instance  ` .

`  database  `

`  string  `

Database name.

`  type  `

`  enum ( DatabaseType  ` )

Type of the Cloud SQL database.

`  credential  `

`  object ( CloudSqlCredential  ` )

Input only. Cloud SQL credential.

`  serviceAccountId  `

`  string  `

Output only. The account ID of the service used for the purpose of this connection.

When the connection is used in the context of an operation in BigQuery, this service account will serve as the identity being used for connecting to the CloudSQL instance specified in this connection.

## DatabaseType

Supported Cloud SQL database types.

Enums

`  DATABASE_TYPE_UNSPECIFIED  `

Unspecified database type.

`  POSTGRES  `

Cloud SQL for PostgreSQL.

`  MYSQL  `

Cloud SQL for MySQL.

## CloudSqlCredential

Credential info for the Cloud SQL.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;username&quot;: string,
  &quot;password&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  username  `

`  string  `

The username for the credential.

`  password  `

`  string  `

The password for the credential.

## AwsProperties

Connection properties specific to Amazon Web Services (AWS).

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{

  // Union field authentication_method can be only one of the following:
  &quot;accessRole&quot;: {
    object (AwsAccessRole)
  }
  // End of list of possible types for union field authentication_method.
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `  authentication_method  ` . Authentication method chosen at connection creation. `  authentication_method  ` can be only one of the following:

`  accessRole  `

`  object ( AwsAccessRole  ` )

Authentication using Google owned service account to assume into customer's AWS IAM Role.

## AwsAccessRole

Authentication method for Amazon Web Services (AWS) that uses Google owned Google service account to assume into customer's AWS IAM Role.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;iamRoleId&quot;: string,
  &quot;identity&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  iamRoleId  `

`  string  `

The user’s AWS IAM Role that trusts the Google-owned AWS IAM user Connection.

`  identity  `

`  string  `

A unique Google-owned and Google-generated identity for the Connection. This identity will be used to access the user's AWS IAM Role.

## AzureProperties

Container for connection properties specific to Azure.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;application&quot;: string,
  &quot;clientId&quot;: string,
  &quot;objectId&quot;: string,
  &quot;customerTenantId&quot;: string,
  &quot;redirectUri&quot;: string,
  &quot;federatedApplicationClientId&quot;: string,
  &quot;identity&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  application  `

`  string  `

Output only. The name of the Azure Active Directory Application.

`  clientId  `

`  string  `

Output only. The client id of the Azure Active Directory Application.

`  objectId  `

`  string  `

Output only. The object id of the Azure Active Directory Application.

`  customerTenantId  `

`  string  `

The id of customer's directory that host the data.

`  redirectUri  `

`  string  `

The URL user will be redirected to after granting consent during connection setup.

`  federatedApplicationClientId  `

`  string  `

The client ID of the user's Azure Active Directory Application used for a federated connection.

`  identity  `

`  string  `

Output only. A unique Google-owned and Google-generated identity for the Connection. This identity will be used to access the user's Azure Active Directory Application.

## CloudSpannerProperties

Connection properties specific to Cloud Spanner.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;database&quot;: string,
  &quot;useParallelism&quot;: boolean,
  &quot;maxParallelism&quot;: integer,
  &quot;useDataBoost&quot;: boolean,
  &quot;databaseRole&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  database  `

`  string  `

Cloud Spanner database in the form \`project/instance/database'

`  useParallelism  `

`  boolean  `

If parallelism should be used when reading from Cloud Spanner

`  maxParallelism  `

`  integer  `

Allows setting max parallelism per query when executing on Spanner independent compute resources. If unspecified, default values of parallelism are chosen that are dependent on the Cloud Spanner instance configuration.

REQUIRES: `  useParallelism  ` must be set.

REQUIRES: `  useDataBoost  ` must be set.

`  useDataBoost  `

`  boolean  `

If set, the request will be executed via Spanner independent compute resources.

REQUIRES: `  useParallelism  ` must be set.

`  databaseRole  `

`  string  `

Optional. Cloud Spanner database role for fine-grained access control. The Cloud Spanner admin should have provisioned the database role with appropriate permissions, such as `  SELECT  ` and `  INSERT  ` . Other users should only use roles provided by their Cloud Spanner admins.

For more details, see [About fine-grained access control](https://cloud.google.com/spanner/docs/fgac-about) .

REQUIRES: The database role name must start with a letter, and can only contain letters, numbers, and underscores.

## CloudResourceProperties

Container for connection properties for delegation of access to GCP resources.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;serviceAccountId&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  serviceAccountId  `

`  string  `

Output only. The account ID of the service created for the purpose of this connection.

The service account does not have any permissions associated with it when it is created. After creation, customers delegate permissions to the service account. When the connection is used in the context of an operation in BigQuery, the service account will be used to connect to the desired resources in GCP.

The account ID is in the form of: @gcp-sa-bigquery-cloudresource.iam.gserviceaccount.com

## SparkProperties

Container for connection properties to execute stored procedures for Apache Spark.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;serviceAccountId&quot;: string,
  &quot;metastoreServiceConfig&quot;: {
    object (MetastoreServiceConfig)
  },
  &quot;sparkHistoryServerConfig&quot;: {
    object (SparkHistoryServerConfig)
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  serviceAccountId  `

`  string  `

Output only. The account ID of the service created for the purpose of this connection.

The service account does not have any permissions associated with it when it is created. After creation, customers delegate permissions to the service account. When the connection is used in the context of a stored procedure for Apache Spark in BigQuery, the service account is used to connect to the desired resources in Google Cloud.

The account ID is in the form of: bqcx- - @gcp-sa-bigquery-consp.iam.gserviceaccount.com

`  metastoreServiceConfig  `

`  object ( MetastoreServiceConfig  ` )

Optional. Dataproc Metastore Service configuration for the connection.

`  sparkHistoryServerConfig  `

`  object ( SparkHistoryServerConfig  ` )

Optional. Spark History Server configuration for the connection.

## MetastoreServiceConfig

Configuration of the Dataproc Metastore Service.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;metastoreService&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  metastoreService  `

`  string  `

Optional. Resource name of an existing Dataproc Metastore service.

Example:

  - `  projects/[projectId]/locations/[region]/services/[serviceId]  `

## SparkHistoryServerConfig

Configuration of the Spark History Server.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;dataprocCluster&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  dataprocCluster  `

`  string  `

Optional. Resource name of an existing Dataproc Cluster to act as a Spark History Server for the connection.

Example:

  - `  projects/[projectId]/regions/[region]/clusters/[cluster_name]  `

## SalesforceDataCloudProperties

Connection properties specific to Salesforce DataCloud. This is intended for use only by Salesforce partner projects.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;instanceUri&quot;: string,
  &quot;identity&quot;: string,
  &quot;tenantId&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  instanceUri  `

`  string  `

The URL to the user's Salesforce DataCloud instance.

`  identity  `

`  string  `

Output only. A unique Google-owned and Google-generated service account identity for the connection.

`  tenantId  `

`  string  `

The ID of the user's Salesforce tenant.

## ConnectorConfiguration

Represents concrete parameter values for Connector Configuration.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;connectorId&quot;: string,
  &quot;endpoint&quot;: {
    object (Endpoint)
  },
  &quot;authentication&quot;: {
    object (Authentication)
  },
  &quot;network&quot;: {
    object (Network)
  },
  &quot;asset&quot;: {
    object (Asset)
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  connectorId  `

`  string  `

Required. Immutable. The ID of the Connector these parameters are configured for.

`  endpoint  `

`  object ( Endpoint  ` )

Specifies how to reach the remote system this connection is pointing to.

`  authentication  `

`  object ( Authentication  ` )

Client authentication.

`  network  `

`  object ( Network  ` )

Networking configuration.

`  asset  `

`  object ( Asset  ` )

Data asset.

## Endpoint

Remote endpoint specification.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{

  // Union field endpoint can be only one of the following:
  &quot;hostPort&quot;: string
  // End of list of possible types for union field endpoint.
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `  endpoint  ` .

`  endpoint  ` can be only one of the following:

`  hostPort  `

`  string  `

Host and port in a format of `  hostname:port  ` as defined in <https://www.ietf.org/rfc/rfc3986.html#section-3.2.2> and <https://www.ietf.org/rfc/rfc3986.html#section-3.2.3> .

## Authentication

Client authentication.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;usernamePassword&quot;: {
    object (UsernamePassword)
  },
  &quot;serviceAccount&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  usernamePassword  `

`  object ( UsernamePassword  ` )

Username/password authentication.

`  serviceAccount  `

`  string  `

Output only. Google-managed service account associated with this connection, e.g., `  service-{project_number}@gcp-sa-bigqueryconnection.iam.gserviceaccount.com  ` . BigQuery jobs using this connection will act as `  serviceAccount  ` identity while connecting to the datasource.

## UsernamePassword

Username and Password authentication.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;username&quot;: string,
  &quot;password&quot;: {
    object (Secret)
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  username  `

`  string  `

Required. Username.

`  password  `

`  object ( Secret  ` )

Required. Password.

## Secret

Secret value parameter.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;secretType&quot;: enum (SecretType),

  // Union field secret can be only one of the following:
  &quot;plaintext&quot;: string
  // End of list of possible types for union field secret.
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  secretType  `

`  enum ( SecretType  ` )

Output only. Indicates type of secret. Can be used to check type of stored secret value even if it's `  INPUT_ONLY  ` .

Union field `  secret  ` . Required. Secret value. `  secret  ` can be only one of the following:

`  plaintext  `

`  string  `

Input only. Secret as plaintext.

## SecretType

Indicates type of stored secret.

Enums

`  SECRET_TYPE_UNSPECIFIED  `

`  PLAINTEXT  `

## Network

Network related configuration.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{

  // Union field network can be only one of the following:
  &quot;privateServiceConnect&quot;: {
    object (PrivateServiceConnect)
  }
  // End of list of possible types for union field network.
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `  network  ` .

`  network  ` can be only one of the following:

`  privateServiceConnect  `

`  object ( PrivateServiceConnect  ` )

Private Service Connect networking configuration.

## PrivateServiceConnect

Private Service Connect configuration.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;networkAttachment&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  networkAttachment  `

`  string  `

Required. Network Attachment name in the format of `  projects/{project}/regions/{region}/networkAttachments/{networkattachment}  ` .

## Asset

Data Asset - a resource within instance of the system, reachable under specified endpoint. For example a database name in a SQL DB.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;database&quot;: string,
  &quot;googleCloudResource&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  database  `

`  string  `

Name of the database.

`  googleCloudResource  `

`  string  `

Full Google Cloud resource name - <https://cloud.google.com/apis/design/resource_names#full_resource_name> . Example: `  //library.googleapis.com/shelves/shelf1/books/book2  `

## Methods

### `             create           `

Creates a new connection.

### `             delete           `

Deletes connection and associated credential.

### `             get           `

Returns specified connection.

### `             getIamPolicy           `

Gets the access control policy for a resource.

### `             list           `

Returns a list of connections in the given project.

### `             patch           `

Updates the specified connection.

### `             setIamPolicy           `

Sets the access control policy on the specified resource.

### `             testIamPermissions           `

Returns permissions that a caller has on the specified resource.
