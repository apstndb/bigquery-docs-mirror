---
name: documents/docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1beta1
uri: https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1beta1
title: Package google.cloud.bigquery.connection.v1beta1
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

## Index

- [`ConnectionService`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1beta1#google.cloud.bigquery.connection.v1beta1.ConnectionService) (interface)
- [`CloudSqlCredential`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1beta1#google.cloud.bigquery.connection.v1beta1.CloudSqlCredential) (message)
- [`CloudSqlProperties`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1beta1#google.cloud.bigquery.connection.v1beta1.CloudSqlProperties) (message)
- [`CloudSqlProperties.DatabaseType`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1beta1#google.cloud.bigquery.connection.v1beta1.CloudSqlProperties.DatabaseType) (enum)
- [`Connection`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1beta1#google.cloud.bigquery.connection.v1beta1.Connection) (message)
- [`ConnectionCredential`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1beta1#google.cloud.bigquery.connection.v1beta1.ConnectionCredential) (message)
- [`CreateConnectionRequest`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1beta1#google.cloud.bigquery.connection.v1beta1.CreateConnectionRequest) (message)
- [`DeleteConnectionRequest`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1beta1#google.cloud.bigquery.connection.v1beta1.DeleteConnectionRequest) (message)
- [`GetConnectionRequest`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1beta1#google.cloud.bigquery.connection.v1beta1.GetConnectionRequest) (message)
- [`ListConnectionsRequest`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1beta1#google.cloud.bigquery.connection.v1beta1.ListConnectionsRequest) (message)
- [`ListConnectionsResponse`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1beta1#google.cloud.bigquery.connection.v1beta1.ListConnectionsResponse) (message)
- [`UpdateConnectionCredentialRequest`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1beta1#google.cloud.bigquery.connection.v1beta1.UpdateConnectionCredentialRequest) (message)
- [`UpdateConnectionRequest`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1beta1#google.cloud.bigquery.connection.v1beta1.UpdateConnectionRequest) (message)

## ConnectionService

Manages external data source connections and credentials.

**CreateConnection**

`rpc CreateConnection( `[`CreateConnectionRequest`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1beta1#google.cloud.bigquery.connection.v1beta1.CreateConnectionRequest)` ) returns ( `[`Connection`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1beta1#google.cloud.bigquery.connection.v1beta1.Connection)` )`

Creates a new connection.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/bigquery`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**DeleteConnection**

`rpc DeleteConnection( `[`DeleteConnectionRequest`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1beta1#google.cloud.bigquery.connection.v1beta1.DeleteConnectionRequest)` ) returns ( `[`Empty`](https://protobuf.dev/reference/protobuf/google.protobuf/#empty)` )`

Deletes connection and associated credential.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/bigquery`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**GetConnection**

`rpc GetConnection( `[`GetConnectionRequest`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1beta1#google.cloud.bigquery.connection.v1beta1.GetConnectionRequest)` ) returns ( `[`Connection`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1beta1#google.cloud.bigquery.connection.v1beta1.Connection)` )`

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

`rpc ListConnections( `[`ListConnectionsRequest`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1beta1#google.cloud.bigquery.connection.v1beta1.ListConnectionsRequest)` ) returns ( `[`ListConnectionsResponse`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1beta1#google.cloud.bigquery.connection.v1beta1.ListConnectionsResponse)` )`

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

`rpc UpdateConnection( `[`UpdateConnectionRequest`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1beta1#google.cloud.bigquery.connection.v1beta1.UpdateConnectionRequest)` ) returns ( `[`Connection`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1beta1#google.cloud.bigquery.connection.v1beta1.Connection)` )`

Updates the specified connection. For security reasons, also resets credential if connection properties are in the update field mask.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/bigquery`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

**UpdateConnectionCredential**

`rpc UpdateConnectionCredential( `[`UpdateConnectionCredentialRequest`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1beta1#google.cloud.bigquery.connection.v1beta1.UpdateConnectionCredentialRequest)` ) returns ( `[`Empty`](https://protobuf.dev/reference/protobuf/google.protobuf/#empty)` )`

Sets the credential for the specified connection.

Authorization scopes  
Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/bigquery`
- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

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
| `type`               | [`DatabaseType`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1beta1#google.cloud.bigquery.connection.v1beta1.CloudSqlProperties.DatabaseType) Type of the Cloud SQL database.                                                      |
| `credential`         | [`CloudSqlCredential`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1beta1#google.cloud.bigquery.connection.v1beta1.CloudSqlCredential) Input only. Cloud SQL credential.                                                           |
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

| Fields                                                                                                                       |                                                                                                                                                                                                                                 |
|------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`                                                                                                                       | `string` The resource name of the connection in the form of: `projects/{project_id}/locations/{location_id}/connections/{connection_id}`                                                                                        |
| `friendly_name`                                                                                                              | `string` User provided display name for the connection.                                                                                                                                                                         |
| `description`                                                                                                                | `string` User provided description.                                                                                                                                                                                             |
| `creation_time`                                                                                                              | `int64` Output only. The creation timestamp of the connection.                                                                                                                                                                  |
| `last_modified_time`                                                                                                         | `int64` Output only. The last update timestamp of the connection.                                                                                                                                                               |
| `has_credential`                                                                                                             | `bool` Output only. True, if credential is configured for this connection.                                                                                                                                                      |
| Union field `properties` . Properties specific to the underlying data source. `properties` can be only one of the following: |                                                                                                                                                                                                                                 |
| `cloud_sql`                                                                                                                  | [`CloudSqlProperties`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1beta1#google.cloud.bigquery.connection.v1beta1.CloudSqlProperties) Cloud SQL properties. |

## ConnectionCredential

Credential to use with a connection.

| Fields                                                                                                                       |                                                                                                                                                                                                                                              |
|------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `credential` . Credential specific to the underlying data source. `credential` can be only one of the following: |                                                                                                                                                                                                                                              |
| `cloud_sql`                                                                                                                  | [`CloudSqlCredential`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1beta1#google.cloud.bigquery.connection.v1beta1.CloudSqlCredential) Credential for Cloud SQL database. |

## CreateConnectionRequest

The request for [`ConnectionService.CreateConnection`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1beta1#google.cloud.bigquery.connection.v1beta1.ConnectionService.CreateConnection) .

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
<td><p><a href="https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1beta1#google.cloud.bigquery.connection.v1beta1.Connection"><code>Connection</code></a></p>
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

The request for [`ConnectionService.GetConnection`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1beta1#google.cloud.bigquery.connection.v1beta1.ConnectionService.GetConnection) .

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

The request for [`ConnectionService.ListConnections`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1beta1#google.cloud.bigquery.connection.v1beta1.ConnectionService.ListConnections) .

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
<td><code>max_results</code></td>
<td><p><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#uint32-value"><code>UInt32Value</code></a></p>
<p>Required. Maximum number of results per page.</p></td>
</tr>
<tr class="odd">
<td><code>page_token</code></td>
<td><p><code>string</code></p>
<p>Page token.</p></td>
</tr>
</tbody>
</table>

## ListConnectionsResponse

The response for [`ConnectionService.ListConnections`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1beta1#google.cloud.bigquery.connection.v1beta1.ConnectionService.ListConnections) .

| Fields            |                                                                                                                                                                                                                |
|-------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `next_page_token` | `string` Next page token.                                                                                                                                                                                      |
| `connections[]`   | [`Connection`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1beta1#google.cloud.bigquery.connection.v1beta1.Connection) List of connections. |

## UpdateConnectionCredentialRequest

The request for [`ConnectionService.UpdateConnectionCredential`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1beta1#google.cloud.bigquery.connection.v1beta1.ConnectionService.UpdateConnectionCredential) .

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
<p>Required. Name of the connection, for example: <code>projects/{project_id}/locations/{location_id}/connections/{connection_id}/credential</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>name</code> :</p>
<ul>
<li><code>bigquery.connections.update</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code>credential</code></td>
<td><p><a href="https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1beta1#google.cloud.bigquery.connection.v1beta1.ConnectionCredential"><code>ConnectionCredential</code></a></p>
<p>Required. Credential to use with the connection.</p></td>
</tr>
</tbody>
</table>

## UpdateConnectionRequest

The request for [`ConnectionService.UpdateConnection`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1beta1#google.cloud.bigquery.connection.v1beta1.ConnectionService.UpdateConnection) .

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
<td><p><a href="https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1beta1#google.cloud.bigquery.connection.v1beta1.Connection"><code>Connection</code></a></p>
<p>Required. Connection containing the updated fields.</p></td>
</tr>
<tr class="odd">
<td><code>update_mask</code></td>
<td><p><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#field-mask"><code>FieldMask</code></a></p>
<p>Required. Update mask for the connection fields to be updated.</p></td>
</tr>
</tbody>
</table>
