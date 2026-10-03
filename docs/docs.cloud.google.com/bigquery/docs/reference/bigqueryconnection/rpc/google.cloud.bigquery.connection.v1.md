---
name: documents/docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1
uri: https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1
title: Package google.cloud.bigquery.connection.v1
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

## Index

- [`ConnectionService`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1#google.cloud.bigquery.connection.v1.ConnectionService) (interface)
- [`AwsAccessRole`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1#google.cloud.bigquery.connection.v1.AwsAccessRole) (message)
- [`AwsProperties`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1#google.cloud.bigquery.connection.v1.AwsProperties) (message)
- [`AzureProperties`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1#google.cloud.bigquery.connection.v1.AzureProperties) (message)
- [`CloudResourceProperties`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1#google.cloud.bigquery.connection.v1.CloudResourceProperties) (message)
- [`CloudSpannerProperties`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1#google.cloud.bigquery.connection.v1.CloudSpannerProperties) (message)
- [`CloudSqlCredential`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1#google.cloud.bigquery.connection.v1.CloudSqlCredential) (message)
- [`CloudSqlProperties`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1#google.cloud.bigquery.connection.v1.CloudSqlProperties) (message)
- [`CloudSqlProperties.DatabaseType`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1#google.cloud.bigquery.connection.v1.CloudSqlProperties.DatabaseType) (enum)
- [`Connection`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1#google.cloud.bigquery.connection.v1.Connection) (message)
- [`ConnectorConfiguration`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1#google.cloud.bigquery.connection.v1.ConnectorConfiguration) (message)
- [`ConnectorConfiguration.Asset`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1#google.cloud.bigquery.connection.v1.ConnectorConfiguration.Asset) (message)
- [`ConnectorConfiguration.Authentication`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1#google.cloud.bigquery.connection.v1.ConnectorConfiguration.Authentication) (message)
- [`ConnectorConfiguration.Endpoint`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1#google.cloud.bigquery.connection.v1.ConnectorConfiguration.Endpoint) (message)
- [`ConnectorConfiguration.Network`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1#google.cloud.bigquery.connection.v1.ConnectorConfiguration.Network) (message)
- [`ConnectorConfiguration.ParameterValue`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1#google.cloud.bigquery.connection.v1.ConnectorConfiguration.ParameterValue) (message)
- [`ConnectorConfiguration.PrivateServiceConnect`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1#google.cloud.bigquery.connection.v1.ConnectorConfiguration.PrivateServiceConnect) (message)
- [`ConnectorConfiguration.Secret`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1#google.cloud.bigquery.connection.v1.ConnectorConfiguration.Secret) (message)
- [`ConnectorConfiguration.Secret.SecretType`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1#google.cloud.bigquery.connection.v1.ConnectorConfiguration.Secret.SecretType) (enum)
- [`ConnectorConfiguration.UsernamePassword`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1#google.cloud.bigquery.connection.v1.ConnectorConfiguration.UsernamePassword) (message)
- [`CreateConnectionRequest`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1#google.cloud.bigquery.connection.v1.CreateConnectionRequest) (message)
- [`DeleteConnectionRequest`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1#google.cloud.bigquery.connection.v1.DeleteConnectionRequest) (message)
- [`GetConnectionRequest`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1#google.cloud.bigquery.connection.v1.GetConnectionRequest) (message)
- [`ListConnectionsRequest`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1#google.cloud.bigquery.connection.v1.ListConnectionsRequest) (message)
- [`ListConnectionsResponse`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1#google.cloud.bigquery.connection.v1.ListConnectionsResponse) (message)
- [`MetastoreServiceConfig`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1#google.cloud.bigquery.connection.v1.MetastoreServiceConfig) (message)
- [`SalesforceDataCloudProperties`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1#google.cloud.bigquery.connection.v1.SalesforceDataCloudProperties) (message)
- [`SparkHistoryServerConfig`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1#google.cloud.bigquery.connection.v1.SparkHistoryServerConfig) (message)
- [`SparkProperties`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1#google.cloud.bigquery.connection.v1.SparkProperties) (message)
- [`UpdateConnectionRequest`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1#google.cloud.bigquery.connection.v1.UpdateConnectionRequest) (message)

## ConnectionService

Manages external data source connections and credentials.

**CreateConnection**

`rpc CreateConnection( `[`CreateConnectionRequest`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1#google.cloud.bigquery.connection.v1.CreateConnectionRequest)` ) returns ( `[`Connection`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1#google.cloud.bigquery.connection.v1.Connection)` )`

Creates a new connection.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/bigquery`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**DeleteConnection**

`rpc DeleteConnection( `[`DeleteConnectionRequest`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1#google.cloud.bigquery.connection.v1.DeleteConnectionRequest)` ) returns ( `[`Empty`](https://protobuf.dev/reference/protobuf/google.protobuf/#empty)` )`

Deletes connection and associated credential.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/bigquery`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**GetConnection**

`rpc GetConnection( `[`GetConnectionRequest`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1#google.cloud.bigquery.connection.v1.GetConnectionRequest)` ) returns ( `[`Connection`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1#google.cloud.bigquery.connection.v1.Connection)` )`

Returns specified connection.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/bigquery`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**GetIamPolicy**

`rpc GetIamPolicy( `[`GetIamPolicyRequest`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.iam.v1#google.iam.v1.GetIamPolicyRequest)` ) returns ( `[`Policy`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.iam.v1#google.iam.v1.Policy)` )`

Gets the access control policy for a resource. Returns an empty policy if the resource exists and does not have a policy set.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/bigquery`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**ListConnections**

`rpc ListConnections( `[`ListConnectionsRequest`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1#google.cloud.bigquery.connection.v1.ListConnectionsRequest)` ) returns ( `[`ListConnectionsResponse`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1#google.cloud.bigquery.connection.v1.ListConnectionsResponse)` )`

Returns a list of connections in the given project.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/bigquery`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**SetIamPolicy**

`rpc SetIamPolicy( `[`SetIamPolicyRequest`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.iam.v1#google.iam.v1.SetIamPolicyRequest)` ) returns ( `[`Policy`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.iam.v1#google.iam.v1.Policy)` )`

Sets the access control policy on the specified resource. Replaces any existing policy.

Can return `NOT_FOUND` , `INVALID_ARGUMENT` , and `PERMISSION_DENIED` errors.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/bigquery`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**TestIamPermissions**

`rpc TestIamPermissions( `[`TestIamPermissionsRequest`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.iam.v1#google.iam.v1.TestIamPermissionsRequest)` ) returns ( `[`TestIamPermissionsResponse`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.iam.v1#google.iam.v1.TestIamPermissionsResponse)` )`

Returns permissions that a caller has on the specified resource. If the resource does not exist, this will return an empty set of permissions, not a `NOT_FOUND` error.

Note: This operation is designed to be used for building permission-aware UIs and command-line tools, not for authorization checking. This operation may "fail open" without warning.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/bigquery`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**UpdateConnection**

`rpc UpdateConnection( `[`UpdateConnectionRequest`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1#google.cloud.bigquery.connection.v1.UpdateConnectionRequest)` ) returns ( `[`Connection`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1#google.cloud.bigquery.connection.v1.Connection)` )`

Updates the specified connection. For security reasons, also resets credential if connection properties are in the update field mask.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/bigquery`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

## AwsAccessRole

Authentication method for Amazon Web Services (AWS) that uses Google owned Google service account to assume into customer's AWS IAM Role.

| Fields        |                                                                                                                                                |
|---------------|------------------------------------------------------------------------------------------------------------------------------------------------|
| `iam_role_id` | `string` The user’s AWS IAM Role that trusts the Google-owned AWS IAM user Connection.                                                         |
| `identity`    | `string` A unique Google-owned and Google-generated identity for the Connection. This identity will be used to access the user's AWS IAM Role. |

## AwsProperties

Connection properties specific to Amazon Web Services (AWS).

| Fields                                                                                                                                               |                                                                                                                                                                                                                                                                                 |
|------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `authentication_method` . Authentication method chosen at connection creation. `authentication_method` can be only one of the following: |                                                                                                                                                                                                                                                                                 |
| `access_role`                                                                                                                                        | [`AwsAccessRole`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1#google.cloud.bigquery.connection.v1.AwsAccessRole) Authentication using Google owned service account to assume into customer's AWS IAM Role. |

## AzureProperties

Container for connection properties specific to Azure.

| Fields                            |                                                                                                                                                                                   |
|-----------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `application`                     | `string` Output only. The name of the Azure Active Directory Application.                                                                                                         |
| `client_id`                       | `string` Output only. The client id of the Azure Active Directory Application.                                                                                                    |
| `object_id`                       | `string` Output only. The object id of the Azure Active Directory Application.                                                                                                    |
| `customer_tenant_id`              | `string` The id of customer's directory that host the data.                                                                                                                       |
| `redirect_uri`                    | `string` The URL user will be redirected to after granting consent during connection setup.                                                                                       |
| `federated_application_client_id` | `string` The client ID of the user's Azure Active Directory Application used for a federated connection.                                                                          |
| `identity`                        | `string` Output only. A unique Google-owned and Google-generated identity for the Connection. This identity will be used to access the user's Azure Active Directory Application. |

## CloudResourceProperties

Container for connection properties for delegation of access to GCP resources.

| Fields               |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
|----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `service_account_id` | `string` Output only. The account ID of the service created for the purpose of this connection. The service account does not have any permissions associated with it when it is created. After creation, customers delegate permissions to the service account. When the connection is used in the context of an operation in BigQuery, the service account will be used to connect to the desired resources in GCP. The account ID is in the form of: @gcp-sa-bigquery-cloudresource.iam.gserviceaccount.com |

## CloudSpannerProperties

Connection properties specific to Cloud Spanner.

| Fields            |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
|-------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `database`        | `string` Cloud Spanner database in the form \`project/instance/database'                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| `use_parallelism` | `bool` If parallelism should be used when reading from Cloud Spanner                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `max_parallelism` | `int32` Allows setting max parallelism per query when executing on Spanner independent compute resources. If unspecified, default values of parallelism are chosen that are dependent on the Cloud Spanner instance configuration. REQUIRES: `use_parallelism` must be set. REQUIRES: `use_data_boost` must be set.                                                                                                                                                                                                        |
| `use_data_boost`  | `bool` If set, the request will be executed via Spanner independent compute resources. REQUIRES: `use_parallelism` must be set.                                                                                                                                                                                                                                                                                                                                                                                            |
| `database_role`   | `string` Optional. Cloud Spanner database role for fine-grained access control. The Cloud Spanner admin should have provisioned the database role with appropriate permissions, such as `SELECT` and `INSERT` . Other users should only use roles provided by their Cloud Spanner admins. For more details, see [About fine-grained access control](https://cloud.google.com/spanner/docs/fgac-about) . REQUIRES: The database role name must start with a letter, and can only contain letters, numbers, and underscores. |

## CloudSqlCredential

Credential info for the Cloud SQL.

| Fields     |                                           |
|------------|-------------------------------------------|
| `username` | `string` The username for the credential. |
| `password` | `string` The password for the credential. |

## CloudSqlProperties

Connection properties specific to the Cloud SQL.

| Fields               |                                                                                                                                                                                                                                                                                                       |
|----------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `instance_id`        | `string` Cloud SQL instance ID in the form `project:location:instance` .                                                                                                                                                                                                                              |
| `database`           | `string` Database name.                                                                                                                                                                                                                                                                               |
| `type`               | [`DatabaseType`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1#google.cloud.bigquery.connection.v1.CloudSqlProperties.DatabaseType) Type of the Cloud SQL database.                                                                |
| `credential`         | [`CloudSqlCredential`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1#google.cloud.bigquery.connection.v1.CloudSqlCredential) Input only. Cloud SQL credential.                                                                     |
| `service_account_id` | `string` Output only. The account ID of the service used for the purpose of this connection. When the connection is used in the context of an operation in BigQuery, this service account will serve as the identity being used for connecting to the CloudSQL instance specified in this connection. |

## DatabaseType

Supported Cloud SQL database types.

| Enums                       |                            |
|-----------------------------|----------------------------|
| `DATABASE_TYPE_UNSPECIFIED` | Unspecified database type. |
| `POSTGRES`                  | Cloud SQL for PostgreSQL.  |
| `MYSQL`                     | Cloud SQL for MySQL.       |

## Connection

Configuration parameters to establish connection with an external data source, except the credential attributes.

| Fields                                                                                                                       |                                                                                                                                                                                                                                                                                                                                                                                                               |
|------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`                                                                                                                       | `string` Output only. The resource name of the connection in the form of: `projects/{project_id}/locations/{location_id}/connections/{connection_id}`                                                                                                                                                                                                                                                         |
| `friendly_name`                                                                                                              | `string` User provided display name for the connection.                                                                                                                                                                                                                                                                                                                                                       |
| `description`                                                                                                                | `string` User provided description.                                                                                                                                                                                                                                                                                                                                                                           |
| `configuration`                                                                                                              | [`ConnectorConfiguration`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1#google.cloud.bigquery.connection.v1.ConnectorConfiguration) Optional. Connector configuration.                                                                                                                                                                    |
| `creation_time`                                                                                                              | `int64` Output only. The creation timestamp of the connection.                                                                                                                                                                                                                                                                                                                                                |
| `last_modified_time`                                                                                                         | `int64` Output only. The last update timestamp of the connection.                                                                                                                                                                                                                                                                                                                                             |
| `has_credential`                                                                                                             | `bool` Output only. True, if credential is configured for this connection.                                                                                                                                                                                                                                                                                                                                    |
| `kms_key_name`                                                                                                               | `string` Optional. The Cloud KMS key that is used for credentials encryption. If omitted, internal Google owned encryption keys are used. Example: `projects/[kms_project_id]/locations/[region]/keyRings/[key_region]/cryptoKeys/[key]`                                                                                                                                                                      |
| Union field `properties` . Properties specific to the underlying data source. `properties` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                                                                               |
| `cloud_sql`                                                                                                                  | [`CloudSqlProperties`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1#google.cloud.bigquery.connection.v1.CloudSqlProperties) Cloud SQL properties.                                                                                                                                                                                         |
| `aws`                                                                                                                        | [`AwsProperties`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1#google.cloud.bigquery.connection.v1.AwsProperties) Amazon Web Services (AWS) properties.                                                                                                                                                                                   |
| `azure`                                                                                                                      | [`AzureProperties`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1#google.cloud.bigquery.connection.v1.AzureProperties) Azure properties.                                                                                                                                                                                                   |
| `cloud_spanner`                                                                                                              | [`CloudSpannerProperties`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1#google.cloud.bigquery.connection.v1.CloudSpannerProperties) Cloud Spanner properties.                                                                                                                                                                             |
| `cloud_resource`                                                                                                             | [`CloudResourceProperties`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1#google.cloud.bigquery.connection.v1.CloudResourceProperties) Cloud Resource properties.                                                                                                                                                                          |
| `spark`                                                                                                                      | [`SparkProperties`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1#google.cloud.bigquery.connection.v1.SparkProperties) Spark properties.                                                                                                                                                                                                   |
| `salesforce_data_cloud`                                                                                                      | [`SalesforceDataCloudProperties`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1#google.cloud.bigquery.connection.v1.SalesforceDataCloudProperties) Optional. Salesforce DataCloud properties. This field is intended for use only by Salesforce partner projects. This field contains properties for your Salesforce DataCloud connection. |

## ConnectorConfiguration

Represents concrete parameter values for Connector Configuration.

| Fields           |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
|------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `connector_id`   | `string` Required. Immutable. The ID of the Connector these parameters are configured for.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| `endpoint`       | [`Endpoint`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1#google.cloud.bigquery.connection.v1.ConnectorConfiguration.Endpoint) Specifies how to reach the remote system this connection is pointing to.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| `authentication` | [`Authentication`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1#google.cloud.bigquery.connection.v1.ConnectorConfiguration.Authentication) Client authentication.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| `network`        | [`Network`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1#google.cloud.bigquery.connection.v1.ConnectorConfiguration.Network) Networking configuration.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| `asset`          | [`Asset`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1#google.cloud.bigquery.connection.v1.ConnectorConfiguration.Asset) Data asset.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| `parameters`     | `map<string, `[`ParameterValue`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1#google.cloud.bigquery.connection.v1.ConnectorConfiguration.ParameterValue)` >` Optional. A map of name-value pairs for connector-specific parameters. These extra configuration parameters aren't standardized in the configuration sections. To update a single parameter value, call [`ConnectionService.UpdateConnection`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1#google.cloud.bigquery.connection.v1.ConnectionService.UpdateConnection) with `update_mask` set to `configuration.parameters.parameter_id` . If `parameter_id` doesn't fit the `[a-zA-Z0-9_]+` pattern, `parameter_id` should be escaped with backticks—for example, `` configuration.parameters.`parameter id` `` . |

## Asset

Data Asset - a resource within instance of the system, reachable under specified endpoint. For example a database name in a SQL DB.

| Fields                  |                                                                                                                                                                                      |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `database`              | `string` Name of the database.                                                                                                                                                       |
| `google_cloud_resource` | `string` Full Google Cloud resource name - <https://cloud.google.com/apis/design/resource_names#full_resource_name> . Example: `//library.googleapis.com/shelves/shelf1/books/book2` |

## Authentication

Client authentication.

| Fields              |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
|---------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `username_password` | [`UsernamePassword`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1#google.cloud.bigquery.connection.v1.ConnectorConfiguration.UsernamePassword) Username/password authentication.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| `service_account`   | `string` Output only. Google-managed service account associated with this connection, e.g., `service-{project_number}@gcp-sa-bigqueryconnection.iam.gserviceaccount.com` . BigQuery jobs using this connection will act as `service_account` identity while connecting to the datasource.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| `parameters`        | `map<string, `[`ParameterValue`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1#google.cloud.bigquery.connection.v1.ConnectorConfiguration.ParameterValue)` >` Optional. A map of name-value pairs for connector-specific parameters. These extra configuration parameters aren't standardized in the configuration sections. To update a single parameter value, call [`ConnectionService.UpdateConnection`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1#google.cloud.bigquery.connection.v1.ConnectionService.UpdateConnection) with `update_mask` set to `configuration.parameters.parameter_id` . If `parameter_id` doesn't fit the `[a-zA-Z0-9_]+` pattern, `parameter_id` should be escaped with backticks—for example, `` configuration.parameters.`parameter id` `` . |

## Endpoint

Remote endpoint specification.

| Fields                                                                |                                                                                                                                                                                       |
|-----------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `endpoint` . `endpoint` can be only one of the following: |                                                                                                                                                                                       |
| `host_port`                                                           | `string` Host and port in a format of `hostname:port` as defined in <https://www.ietf.org/rfc/rfc3986.html#section-3.2.2> and <https://www.ietf.org/rfc/rfc3986.html#section-3.2.3> . |

## Network

Network related configuration.

| Fields                                                              |                                                                                                                                                                                                                                                                                |
|---------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `network` . `network` can be only one of the following: |                                                                                                                                                                                                                                                                                |
| `private_service_connect`                                           | [`PrivateServiceConnect`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1#google.cloud.bigquery.connection.v1.ConnectorConfiguration.PrivateServiceConnect) Private Service Connect networking configuration. |

## ParameterValue

Represents a value for a connector parameter.

| Fields                                                        |                                                                                                                                                                                                                                                                      |
|---------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `kind` . `kind` can be only one of the following: |                                                                                                                                                                                                                                                                      |
| `string_value`                                                | `string` A string parameter value.                                                                                                                                                                                                                                   |
| `bool_value`                                                  | `bool` A boolean parameter value.                                                                                                                                                                                                                                    |
| `int32_value`                                                 | `int32` An int32 parameter value.                                                                                                                                                                                                                                    |
| `double_value`                                                | `double` A double parameter value.                                                                                                                                                                                                                                   |
| `secret_value`                                                | [`Secret`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1#google.cloud.bigquery.connection.v1.ConnectorConfiguration.Secret) A secret parameter value. Allowed only for Authentication parameters. |

## PrivateServiceConnect

Private Service Connect configuration.

| Fields               |                                                                                                                                            |
|----------------------|--------------------------------------------------------------------------------------------------------------------------------------------|
| `network_attachment` | `string` Required. Network Attachment name in the format of `projects/{project}/regions/{region}/networkAttachments/{networkattachment}` . |

## Secret

Secret value parameter.

| Fields                                                                                    |                                                                                                                                                                                                                                                                                                                                   |
|-------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `secret_type`                                                                             | [`SecretType`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1#google.cloud.bigquery.connection.v1.ConnectorConfiguration.Secret.SecretType) Output only. Indicates type of secret. Can be used to check type of stored secret value even if it's `INPUT_ONLY` . |
| Union field `secret` . Required. Secret value. `secret` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                   |
| `plaintext`                                                                               | `string` Input only. Secret as plaintext.                                                                                                                                                                                                                                                                                         |

## SecretType

Indicates type of stored secret.

| Enums                     |     |
|---------------------------|-----|
| `SECRET_TYPE_UNSPECIFIED` |     |
| `PLAINTEXT`               |     |

## UsernamePassword

Username and Password authentication.

| Fields     |                                                                                                                                                                                                                    |
|------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `username` | `string` Required. Username.                                                                                                                                                                                       |
| `password` | [`Secret`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1#google.cloud.bigquery.connection.v1.ConnectorConfiguration.Secret) Required. Password. |

## CreateConnectionRequest

The request for [`ConnectionService.CreateConnection`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1#google.cloud.bigquery.connection.v1.ConnectionService.CreateConnection) .

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>parent</code></td>
<td><p><code>string</code></p>
<p>Required. Parent resource name. Must be in the format <code>projects/{project_id}/locations/{location_id}</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>parent</code> :</p>
<ul>
<li><code>bigquery.connections.create</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code>connection_id</code></td>
<td><p><code>string</code></p>
<p>Optional. Connection id that should be assigned to the created connection.</p></td>
</tr>
<tr class="odd">
<td><code>connection</code></td>
<td><p><a href="https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1#google.cloud.bigquery.connection.v1.Connection"><code>Connection</code></a></p>
<p>Required. Connection to create.</p></td>
</tr>
</tbody>
</table>

## DeleteConnectionRequest

The request for \[ConnectionService.DeleteConnectionRequest\]\[\].

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>name</code></td>
<td><p><code>string</code></p>
<p>Required. Name of the deleted connection, for example: <code>projects/{project_id}/locations/{location_id}/connections/{connection_id}</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>name</code> :</p>
<ul>
<li><code>bigquery.connections.delete</code></li>
</ul></td>
</tr>
</tbody>
</table>

## GetConnectionRequest

The request for [`ConnectionService.GetConnection`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1#google.cloud.bigquery.connection.v1.ConnectionService.GetConnection) .

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>name</code></td>
<td><p><code>string</code></p>
<p>Required. Name of the requested connection, for example: <code>projects/{project_id}/locations/{location_id}/connections/{connection_id}</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>name</code> :</p>
<ul>
<li><code>bigquery.connections.get</code></li>
</ul></td>
</tr>
</tbody>
</table>

## ListConnectionsRequest

The request for [`ConnectionService.ListConnections`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1#google.cloud.bigquery.connection.v1.ConnectionService.ListConnections) .

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>parent</code></td>
<td><p><code>string</code></p>
<p>Required. Parent resource name. Must be in the form: <code>projects/{project_id}/locations/{location_id}</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>parent</code> :</p>
<ul>
<li><code>bigquery.connections.list</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code>page_size</code></td>
<td><p><code>int32</code></p>
<p>Required. Page size.</p></td>
</tr>
<tr class="odd">
<td><code>page_token</code></td>
<td><p><code>string</code></p>
<p>Page token.</p></td>
</tr>
</tbody>
</table>

## ListConnectionsResponse

The response for [`ConnectionService.ListConnections`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1#google.cloud.bigquery.connection.v1.ConnectionService.ListConnections) .

| Fields            |                                                                                                                                                                                                      |
|-------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `next_page_token` | `string` Next page token.                                                                                                                                                                            |
| `connections[]`   | [`Connection`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1#google.cloud.bigquery.connection.v1.Connection) List of connections. |

## MetastoreServiceConfig

Configuration of the Dataproc Metastore Service.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>metastore_service</code></td>
<td><p><code>string</code></p>
<p>Optional. Resource name of an existing Dataproc Metastore service.</p>
<p>Example:</p>
<ul>
<li><code>projects/[project_id]/locations/[region]/services/[service_id]</code></li>
</ul></td>
</tr>
</tbody>
</table>

## SalesforceDataCloudProperties

Connection properties specific to Salesforce DataCloud. This is intended for use only by Salesforce partner projects.

| Fields         |                                                                                                               |
|----------------|---------------------------------------------------------------------------------------------------------------|
| `instance_uri` | `string` The URL to the user's Salesforce DataCloud instance.                                                 |
| `identity`     | `string` Output only. A unique Google-owned and Google-generated service account identity for the connection. |
| `tenant_id`    | `string` The ID of the user's Salesforce tenant.                                                              |

## SparkHistoryServerConfig

Configuration of the Spark History Server.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>dataproc_cluster</code></td>
<td><p><code>string</code></p>
<p>Optional. Resource name of an existing Dataproc Cluster to act as a Spark History Server for the connection.</p>
<p>Example:</p>
<ul>
<li><code>projects/[project_id]/regions/[region]/clusters/[cluster_name]</code></li>
</ul></td>
</tr>
</tbody>
</table>

## SparkProperties

Container for connection properties to execute stored procedures for Apache Spark.

| Fields                        |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
|-------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `service_account_id`          | `string` Output only. The account ID of the service created for the purpose of this connection. The service account does not have any permissions associated with it when it is created. After creation, customers delegate permissions to the service account. When the connection is used in the context of a stored procedure for Apache Spark in BigQuery, the service account is used to connect to the desired resources in Google Cloud. The account ID is in the form of: bqcx- - @gcp-sa-bigquery-consp.iam.gserviceaccount.com |
| `metastore_service_config`    | [`MetastoreServiceConfig`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1#google.cloud.bigquery.connection.v1.MetastoreServiceConfig) Optional. Dataproc Metastore Service configuration for the connection.                                                                                                                                                                                                                                                           |
| `spark_history_server_config` | [`SparkHistoryServerConfig`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1#google.cloud.bigquery.connection.v1.SparkHistoryServerConfig) Optional. Spark History Server configuration for the connection.                                                                                                                                                                                                                                                             |

## UpdateConnectionRequest

The request for [`ConnectionService.UpdateConnection`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1#google.cloud.bigquery.connection.v1.ConnectionService.UpdateConnection) .

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>name</code></td>
<td><p><code>string</code></p>
<p>Required. Name of the connection to update, for example: <code>projects/{project_id}/locations/{location_id}/connections/{connection_id}</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>name</code> :</p>
<ul>
<li><code>bigquery.connections.update</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code>connection</code></td>
<td><p><a href="https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1#google.cloud.bigquery.connection.v1.Connection"><code>Connection</code></a></p>
<p>Required. Connection containing the updated fields.</p></td>
</tr>
<tr class="odd">
<td><code>update_mask</code></td>
<td><p><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#field-mask"><code>FieldMask</code></a></p>
<p>Required. Update mask for the connection fields to be updated.</p></td>
</tr>
</tbody>
</table>
